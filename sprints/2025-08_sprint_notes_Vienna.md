# skimage team meeting, August 2025, Vienna

:::info
**Venue:** Zoku, Perspektivstr. 6, 1020 Wien, Austria
**Dates:** 14, 15, 16 August 2025

**Attendees:**

- Grzegorz Bokota (at EuroSciPy afterwards)
- Matthew Brett
- Marianne Corvellec
- Lars Grüter (at EuroSciPy afterwards)
- Juan Nunez-Iglesias
- Stéfan van der Walt (at EuroSciPy afterwards)
:::

## Agenda

### Day 1 (Thursday)

- [name=Lars] Update on skimage2 presentation
  - Current strategy ([discussion](https://discuss.scientific-python.org/t/a-pragmatic-pathway-towards-skimage2/530))
  - Progress
  - Common skimage2 patterns
  - Funding status

- **Prescale / input_range / preserve_range**
  - After discussion: decided on more explicit naming using `input_range=` rather than `prescale=`. `input_range='auto'` or `input_range` required as skimage2 default (`prescale='legacy'` skimage1 default).
    - `blob_funcs`

- **Colorspace conversions**
    - we need to look at common definitions of color spaces – if they assume anything about the (output) value range. If input would lead to invalid / unconventional output in a specific color space, raise an explicit error or warning
  - discussion on expected value ranges: https://github.com/scikit-image/scikit-image/issues/1185

- **Overarching goals / By the end of the sprint**
    - import (and call) at least one function from `skimage2` that is different from its `skimage1` version
    - have corresponding documentation in the skimage to skimage2 migration guide

- **Naming of `transform.*` functions**: spatial transformations, value-based transformations such as Hough, radon, pyramid

### Day 2 (Friday)

- Coordinate conventions (see write-up below)
- Finalize src + skimage2 package refactor + CI
  - Nightly wheel building
  - Data fetcher

### Day 3 (Saturday) 🥲

- AI slop measure
- docstub
- SKIP 4
- Photo
- Funding / pace

### Discussions

- Roadmap to scikit-image 2.0 ([master document](https://hackmd.io/iaYwrYTZQeuokOtLhT9KZA) from 2024 in-person sprint: taken over by [wiki page](https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2))
  - [name=Matthew] Coordinate conventions
    - example issue caused by the xy/rc mismatch https://github.com/jni/affinder/issues/61#issuecomment-1091246577
  - Value-range scaling
    - [Why `preserve_range` is not enough](https://hackmd.io/hX8GftVsQcKfDa3NBXxQow)
  - typing and protocols
    - [Discussion: NewType vs Annotated](https://discuss.scientific-python.org/t/typing-scikit-image/877)
- [name=Lars] [Docstub](https://github.com/scientific-python/docstub) conventions
  - natural language array format
      - [typing syntax](https://github.com/scientific-python/docstub/blob/main/docs/typing_syntax.md)
      - note "Python's typing system does not support yet expressing the shape of an array" -- [name=Grzegorz] says it does now
  - TODO Sequence vs Sized vs tuple...
  - Generics in docstrings?
      - available from Python 3.12?
      - let skimage2 only support Python>=3.12
          - https://scientific-python.org/specs/spec-0000/ (can drop 3.11 soon)
  - [natural language callables](https://github.com/scientific-python/docstub/issues/11)?
    `callable[[int, float], str]` (int, float) -> str 
     ( type [, type]+ ) -> type
  - complicated types exceeding line limit?
- Dispatching
    - a team prototyped it in NetworkX and in scikit-image
    - now turning into the [spatch](https://github.com/scientific-python/spatch) project
- Uncoupling deprecation policy from release cycle
    - Safe to bump version back of actual deprecated version
- Funding
  - Going into 2026 
  - Funding Peter Rush's work on Scientific Python lectures
    - 5k committed
  - Contracts & NCE
- [Logo redesign](https://discuss.scientific-python.org/t/scikit-image-logo-redesign/536)
    - We'll ask designer to take a look and refine Lars's design
- AI contributions
  - https://github.com/scientific-python/summit-2025/issues/35
  - https://github.com/matthew-brett/sp-ai-post/blob/main/notes.md
  - [name=Matthew] it's okay to use AI for mechanical tasks (e.g., reordering imports): "this refactoring is so straightforward that there cannot be any copyright infringement".  Otherwise (there are non-mechanical not-obvious changes) the submitter who has used AI has to make the argument that the changes do not violate any copyright.

- When using an `skimage` (v1) function that has been ported, it will raise a warning telling you how to port it to `skimage2`. This warning can be suppressed, and the migration guide tells users how.

## Blob detection functions

We discussed an algorithm that would allow a sensible `threshold` for the blob detection functions.   The functions in question are `blob_dog` (difference of Gaussians), `blob_log` (Laplacian of Gaussians) and `blob_doh` (determinant of Hessians). All three functions have default `threshold`s, designed to be useful for images in the range [0, 1].

Bear in mind that both functions, now, apply what we will call scikit-image 1 scaling (SK1 scaling) to the images, before further calculation.  The algorithm for SK1 scaling is:

* Do no scaling on float
* Scale int images such that the *dtype max* maps to 1, and the *dtype min* maps to -1.
* Scale uint images such that the *dtype max* maps to 1, and 0 maps to 0.

Consider `blob_dog`.  After scaling, as applied above, the routine calculates a *stack* (3D array) of k slices size M, N, where the original input image is size M, N.  These k images are difference of Gaussian images.  The `threshold` value applies to these derived images.

The problem is that the SK1 scaling is a) difficult to explain b) isn't expected to work with the default threshold when the floating point images are not in the range [0, 1] and c) may not be sensible for scaling integer images that don't fill most of their range, such as `int32` images with max << $2^{31}$.

We therefore iterated to a proposed replacement for this behavior with the hope that it will give reasonable results for a wider range of images, and in particular, to floating point images not already in the range [0, 1].

To do this, we introduce a new keyword `prescale` which can take the following values:

* `prescale='minmax'` - see below.
* `prescale='legacy'` - applies SK1 scaling as above.
* `prescale=(c, d)` - (a tuple of values) - see below.
* `prescale='none'` - apply no scaling to the image.

`prescale='minmax'` is equivalent to setting `prescale=(img.min(), img.max())`.

`prescale=(c, d)` scales the values in image with `(img - c) / (d - c)`, such that value `c` in the original image maps to 0, and value `d` maps to 1.  Therefore `threshold` applies to the derived image stack (see above) calculated from the image scaled in this way.

We will raise an error when `c >= d` (and therefore when `prescale='minmax'` and `img.min == img.max`).

We should:

* Write tests to assure ourselves that `prescale` options work as expected on `int` and `uint` images, and with floats of arbitrary range (range other than [0, 1]).
* Check and test the gallery images applying these functions.
* Write examples that use manual scaling (prescale=(c, d))

## A policy for skimage2

Installing `skimage` will install two namespaces:

- `skimage` (call this the Scikit-Image 1 namespace - SK1).
- `skimage2` (call this the Scikit-Image 2 namespace - SK2).

As a general rule *it should always be possible to achieve the current behavior of SK1 by some call or set of calls to SK2.*

(There may be some situations where we have to break this general rule, but the argument should be made for the relevant API change that breaks the rule.)

Consider the function `skimage.feature.blob_dog` - see above.  At the moment one could call this with:

```
A = skimage.feature.blob_dog(img)
```

Where the `img` input is scaled according the SK1 standard scaling rules, before calculating the stack of Gaussian difference images, and then applying the default threshold value (0.5) to detect candidate blobs.

As discussed above, we propose addinging a `prescale` keyword argument to `blob_dog`, defaulting to `prescale='normalize'` - giving behavior that SK1 does not have.

The rule above means that there must be a way to replicate the current SK1 default behavior with SK2.  So, any call of `skimage.feature.blob_dog`, regardless of input arguments, will give a deprecation warning of form:

> We are porting `skimage.feature.blob_dog` to the `skimage2` namespace, as `skimage2.feature.blob_dog`.  However, the default behavior of the `skimage2` version differs from that of `skimage`.  Please check the docstring of the `skimage2.feature.blob_dog` function for possible ways to improve your call of this code, but to replicate the default behavior of `skimage`, use:
> 
> ```
    > A = skimage2.feature.blob_dog(img, ..., prescale='legacy', ...)
> ```

## Coordinate systems

Skimage spatial transforms implement various coordinate transforms.

These are agnostic to the meaning of the particular axes.  There is a first axis, and a second axis, and maybe a third.  The user could be thinking of these axes as:

* First axis x - columns.
* Second axis y - rows.

This is the "xy" - or image processing convention.

or:

* First axis i - rows.
* Second axis j - columns.

This is the "ij" or "rc" Numpy convention.

~~In either case, we have a right-handed coordinate system.  For "xy", we can think of the z (third) axis as pointing away from the viewer, and positive rotation will, when applied, be clockwise.~~

~~Conversely, for "ij", we can think of the z (third) axis as pointing towards the viewer, and positive rotation will, when applied, be anti-clockwise.~~

The `transform` classes are consistent, in that they then apply, via `__call__`, to a 2D or 3D coordinate array, where the first column of the array corresponds to coordinates on the first axis.   Thus one would pass transforms intended to operate on "xy" a 2D coordinate array where the first column gives column coordinates, and the second gives row coordinates.

All this to say that the transform classes are self-consistent, and are therefore agnostic about their coordinate systems, and need no update for "ij" use. :+1: 

However, when we apply these transforms to images, for example in `skimage.transform.warp`, we do need to know what the first axis means in terms of the image coordinates.  See the docstring description of the `inverse_map` parameter of `warp`.

This also applies to `skimage.transform.warp_coords`. And probably others.

We determined the upgrade path from SK1 to SK2 would be to suggest (e.g. for `warp`):

> You can get the same behavior as SK1, with SK2, by applying an axis flipping transform to the input transform.  Therefore:
>
> out = skimage.transform.warp(img, tform)
>
> becomes:
>
> out = skimage2.transform.warp(img, permute_axes(tform))
> out = skimage2.transform.warp(img, PermuteAxes(to=(1, 0)) @ tform)
> out = skimage2.transform.warp(img, xy_to_ij(tform))

We discussed adding something like `coord_sys` keyword argument to e.g. `warp`.  `coord_sys='ij'` would be the default, but `coord_sys='xy'` would give the SK1 behavior.  We concluded that this would be little benefit for some cost, as we would want to deprecate and remove `coord_sys` keyword argument in due course.

We also found `shift_x` and `shift_y` parameters in the following public `skimage.filters.rank` modules:

* `_percentile`
* `_generic`
* `bilateral`
 
`shift_x` appears to refer to shifts in columns, and `shift_y` to rows.  These need to be modified to be e.g. `shift=(r, c)`.

We should investigate use of variable names / docstring uses of `shear_x`, `shear_y`, `translate_x`, `translate_y` in the `transform._geometric` module; it looks like these will pan out to be `shear_ax0`, `shear_ax1`, but let's confirm.


## Typing, docstub & doctype conventions

- Array format in scikit-image?

  - skimage should use scikit-learn conventions `array of shape S and dtype D`
    `2-D array` - not sure if we 
  - `array` (i.e., any array) vs `ndarray` (i.e., a NumPy array) vs `array-like` (i.e., anything that can be coerced into a NumPy array)
      - we don't want to support, say, only Dask arrays and *not* NumPy arrays

- Narrow or general types? E.g. `Sequence` vs `list`?
  - try to use the more general type!
  - But require `array` for things that might be big, `array-like` is allowed for very small input that is convenient to be type as e.g. `[1, 2, 1]`.

- Natural language form for callables?
  - `(int, /, x=float, *, y=str) -> int`

- Typing with NumPy now supports shape? -> Yes!

- How could we encode overloading in docstrings with docstub?
  - Maybe use something like
    ```
    def foo(img, mask):
        """
        img : array of shape (T, K[, P])
        mask : array of shape (T, K[, P]) as `img`
        """
    ```
    which will tell docstub that the shape `(T, K)` and `(T, K, P)` should be in sync for the parameters `img` and `mask`?


- Annotating arrays
  - How can we encode a parameter accepting something like a `Mask` 


- Dtype nicknames
  - "np.int" = "np.integer" or maybe "~int" = "np.integer"
  - "uint8" = "np.uint8"
