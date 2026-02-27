# Why `preserve_range` is not enough

:::: info
**Authors:** Stéfan van der Walt, Matthew Brett, Lars Grüter
**Date:** 2025-07-23
::::

In scikit-image 1.0, we have the convention that all floating-point images are in `[0, 1]`.
Unfortunately, we never enforced this — however, you quickly run into difficulties when you go against the convention.

In scikit-image 2.0, we aim to lift this restriction, so that users can operate on images (integer or float) without restricting the range of values. For floating-point images, this means internally that functions must now handle data ranges other than `[0, 1]`.
For integer images, it means that we will no longer normalize, using the data-type range, to `[0, 1]` (for unsigned integer images) or `[-1, 1]` (for signed integer images) (see below).

The `preserve_range` keyword argument was introduced quite a while ago to make this future transition easier:
when presented with a floating-point image, it allows it through unmodified.
When presented with an integer image, `preserve_range=False` rescales that image to `[0, 1]` or `[-1, 1]`, or when `preserve_range=True` lets it through unmodified (though may cast to `float` for internal computation).
This behavior can be pretty confusing, since `preserve_range=False` *seems* to tell the user that *all* inputs (float or integer) will be scaled.

## The current (1.0) algorithm for scaling images

See `skimage.util.dtype.img_as_float`, and associated functions.  We pass through floating-point images unmodified (although we may cast to higher precision float).   We rescale `int` images by dividing by the `dtype` maximum of the `int` type, and then clipping any values below -1, to -1.  This scales `int` images to the range `[-1, 1]`, where a rescaled value of 1 corresponds to an original value that was the maximum of the `dtype`.   For example, for an input `int8` image, `img_as_float` will map 127 to 1, -128 and -127 to -1.  If we have an `int32` image, then a value of, say, 100,000 will get mapped to 100,000 / (2 ** 31 - 1) = 0.000046.   We also rescale `uint` images by dividing by the `dtype` max, so 0 maps to 0, and `np.iinfo(dt).max`  maps to 1.  For `uint8`, 255 maps to 1.  For `uint32`, 100,000 maps to 0.00023. (Clearly, `uint32` is not a practical dtype in the current scheme of things.)

## The problem

There are two classes of functions in scikit-image: those that care about the input range, and those that don't.
In fact, few functions need to know the input range, but for those that do it is crucial.
For example, consider a function that allows the user to specify a threshold.
This threshold is only useful if it is fairly robust to the input dtype and range of data, i.e. is intuitively predictive of the outcome, or applies to a large batch of images.
When images are in the range `[0, 1]`, or normalized to be so, then thresholds naturally fall in that same range.
However, now we have to deal with images with a wider range of values; in general, how do we allow the intuitive specification of thresholds?

## Presented solution

We recommend introducing a new `prescale` argument to functions that care about data range.
This argument will tell the function how to normalize input data, so that function parameters can be set in an intuitive way (not varying depending on input image range).

If `preserve_range` had richer semantics, we could have used it instead.
However, as it is, all it does is allow us to be *presented* with the problem described above (a wide range of input values).
In scikit-image 2.0, `preserve_range` will be True everywhere (implied, the keyword itself will be removed), and therefore the problem will be pervasive.

Consider the threshold-setting example above, which we believe represents the issue for a wider set of functions.
There are at least three ways of making the threshold more predictable: (1) ask the user to normalize data beforehand (2) normalize the image data internally to the function (this is the approach we take in 1.0, for ints, but not for floats) or (3) keep the data as-is, but use the data range (potentially some data range that takes into account we will be sending a series of different images that need thresholding), to calculate an absolute threshold (in the scale of the original data) corresponding to a relative threshold for data scaled to `[0, 1]` or `[-1, 1]`.

(3) may be possible, depending on the algorithm, and (1) would depend fully on the user, so we consider (2) to be our easiest (and, for the user, most convenient) route forward.

How this would look:

1. **Single image:** `blob_doh(input_image, prescale='normalize', threshold=0.1)`

   Image is normalized to `[0, 1]`, using `min` and `max` values, for all images, including floating-point images and unsigned integers (that would previously have been scaled to `[-1, 1]`).

2. **Backward compatible:** `blob_doh(input_image, prescale='legacy', threshold=0.1)`

   Current 1.0 behavior; user can use this to port existing code.
Floating-point images should be in `[0, 1]` per convention, integer images will be rescaled by data-type as above.
This mode could also be called `int_only`, `int_dt_max`, or `normalize_by_dtype`.

3. **Batch of images:** `blob_doh(input_image, prescale=('normalize', -10, 100), threshold=0.1)`

   We're operating on a batch of images from, say, a thermal camera.
We know the temperature values are between -10 and 100.
Images are normalized, using `(img - (-10))/(100 - (-10))` (shifted and scaled), so that the threshold remains intuitive.

4. **Advanced:** `blob_doh(input_image, prescale='none', threshold=25)`

   We are working with a batch of thermal imaging data, ranging from -10 to 100.
We know that, in the Hessian feature space, values are squared.
Therefore, we pre-compute a threshold in that space of 5*5 = 25.

   Of course, the user could also scale the images in some suitable way before sending them to the (e.g.) `blob_doh` function.
   
   We could also imagine, perhaps at some later point, allowing `prescale=my_func`, where `my_func` is some function that accepts an image (an array) and returns a scaled image.  We could extend this to allow e.g. `prescale=(my_func, -10, 100)`, that would result in the internal call `new_img = my_func(input_img, *args)`, where `args` in this case would be `(-10, 100)`.  However, this API takes us close to or past the point at which it would be clearer for the user to simply do that scaling themselves, before calling e.g. `blob_doh`.

## Implementation

There should be a single shared function to implement the behavior of the `prescale=` parameter consistently. We may choose to make it public. E.g.

```python
# in skimage.util
def prescale(image, PRESCALE_TYPE): ...
```

Prescaling could also be formulated as a decorator:

```python
@prescale
def blob_doh(prescaled_image, ...): ...
```

## Notes and comments

- Prescaling has a non-trivial cost, especially across a batch, so that would be one argument for encouraging users to prescale data and use `prescale='none'`. This is one argument in favor of a public utility function.

# Discussion

At the sprint, this proposal was discussed. The team felt that `input_range` is more intuitive. It would have options `"auto"`, `"legacy"`, and also accept a tuple. Anything more fancy can be implemented by the user outside the function.

`skimage1` would have `"legacy"` as default; `skimage2` can have `"auto"` as default, or require the argument to be set explicitly.

There are some existing `in_range` arguments that need to be updated to `input_range` (see [rescale_intensity](https://scikit-image.org/docs/stable/api/skimage.exposure.html#skimage.exposure.rescale_intensity)).
