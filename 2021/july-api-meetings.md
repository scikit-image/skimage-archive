# skimage 1.0 API changes notes

issue: https://github.com/scikit-image/scikit-image/issues/5439

## 1. Europe/Asia

Present: Marianne, Juan
Meeting date: 2021-07-01 at 10:00 CEST

- Juan likes Marianne's proposal to add channel_axis to functions that assume final channel axis: https://github.com/scikit-image/scikit-image/issues/5439#issuecomment-867547754

- Marianne agrees with preserve_range default + documentation about exposure.rescale_intensity. img_as_float & co should go to `.astype(float)` + rescale_intensity. [#3373](https://github.com/scikit-image/scikit-image/issues/3373) can be decided on a case-by-case basis. Worst case, range can be introspected, even if slow.

- Before launch of 0.20, migration guide landing page should be ready
- Before launch of 1.0, there should be a "migration freeze" of ~1mo, where migration guide is complete and (maybe) 0.21 is released with new warning. This will help people who want to migrate but come to the page too early. Should be Oct/Nov so that Europeans are not on holiday

- regionprops consistent naming: Marianne and Juan both think that consistency might not be the only/best constraint: it should read as good English. "intensity_min" is not as natural as "min_intensity", for example. Do we reconsider this move?

- Oldest (maybe) living issue: https://github.com/scikit-image/scikit-image/issues/1234 Our 'conversion' functions live in util, exposure but also in the base name space (which isn't great). By now, Marianne is in favour of renaming 'conversion' functions into `rescale_to_*`. Juan however thinks that e.g. `rescale_intensity(image, in_range=image.dtype.type, out_range=float)` might be enough. Marianne agrees but suggests we need to be able to control both output dtype *and* output range independently. This could be done by adding a `dtype=` kwarg to `rescale_intensity`. `rescale_intensity(image, in_range=image.dtype.type, out_range=(0, 2.5), dtype=np.float32)`. We could also simplify so that `image.dtype` by itself works. (currently raises `TypeError: cannot unpack non-iterable numpy.dtype[uint8] object`). Single function, reads nicely, and everything is nice and explicit.

- We decided long ago on label_image to distinguish from e.g. the unique labels present in an image. However Juan would not be opposed to reversing this decision. Marianne suggests that `labels` is actually more common so it would be a smaller change. A crazy proposal from Juan: change the parameter name to `segmentation`, then rethink module names. But btw napari uses `labels` for this type of data structure.

- in https://github.com/scikit-image/scikit-image/issues/4876, François pointed out that `num_workers` is more explicit as one knows that one has to pass in an integer. But Alex notes that consistency with the ecosystem is a good goal, and Juan and Marianne agree. Additionally, we can envision a future where `workers=` can take in other arguments such as a dask scheduler.

- `random_seed` is most explicit/commonly understood. Juan feels `random_state` is a bit more obscure for people who don't know about RNGs (including past Juan) https://github.com/scikit-image/scikit-image/issues/5359 Marianne suggests this makes a nice work item with the unification of all the random number generation in the library (see todos section)

- Marianne thinks that bullet points "label_image vs labels as a parameter name: issue #?" falls under broader point "Update API for skimage.future.graph.RAG" https://github.com/scikit-image/scikit-image/issues/1696

- RAG issues https://github.com/scikit-image/scikit-image/issues/1696 Juan was working on cleaning up the API but got stuck when he couldn't make an existing test pass. It turns out that the merging has a bug in it, see https://github.com/scikit-image/scikit-image/issues/5360, so maybe the test itself needed updating. Juan will investigate again. (see todos)

- People have been confused before by imageio vs skimage.io. Additionally, imagecollection's behaviour with multipage tiffs is strange and hard to predict. Our plugin infrastructure is rather old fashioned. Overall it seems to Juan & Marianne that this functionality is independent of image processing/analysis and should thus live separately. imageio seems like the natural fit. Stéfan has misgivings about the direction of the imageio API but we have control over that, even if we haven't exercised it yet. Almar Klein is open to moving imageio under the skimage umbrella. Also Marianne suggests we could move our *own* io submodule into a different package, if we decide we don't want the imageio API. e.g. `pip install scikit-image[io]`

- both happy to remove skimage.viewer. napari offers all its functionality.

- Marianne brought up metadata (😡) (https://github.com/scikit-image/scikit-image/issues/2605), but Juan thinks that we can't solve it before 1.0. However, we should keep it in mind when designing the API, so that future improvements can be added in a backwards compatible way.

- For API grouping and unification (https://github.com/scikit-image/scikit-image/issues/5439#issuecomment-866642190), Marianne suggests maybe Gephi for moving the functions around in 2D space and link them? Or cytoscape.

## 2. US/Europe

Present: Marianne,
Meeting date: 2021-07-01 at 09:00 EDT

- 

## immediate todos

- review/approve/merge https://github.com/scikit-image/scikit-image/pull/5444
- random number generator always uses unified API. https://github.com/scikit-image/scikit-image/issues/5357 Some bits were missing from that PR (use `git grep` to find them). Nice place to unify `random_seed=` or `random_state=` keyword.
- review/approve/merge https://github.com/scikit-image/scikit-image/pull/4482
- Juan: finish RAG migration from skimage.future.
