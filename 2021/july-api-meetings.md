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

Present: Marianne, Mark

Meeting date: 2021-07-01 at 09:00 EDT

- Metadata:
    - Still a big issue. Probably not for us :D.
- Marianne explains: 
    - 0.19 release is "normal",
    - 0.20 is "dummy" in the sense that it is the same as 0.19, but with the dependency warning ("use `skimage<0.20.0` if you don't want to update your code, otherwise follow this migration guide").
        - Gives users a migration guide.
        - At first, migration guide is not "comprehensive" because it cannot anticipate all the challenges that users will encounter.
    - Mark: How can we be **dynamic** with the comprehensive guide?
        - Marianne: We will need to move quite fast.
        - Mark: My last attempt at improving a guide (i.e., the install guide), was in my mind "better" at some point, but never perfect. I felt like it took too long to become "public" when somebody else had the bandwidth to improve it even more.
        - Mark: Can we use the wiki, to stage?
            - Ask community to open issues with suggestions if they can't edit?
            - Can the community contribute to the Wiki?
    - Mark: One big challenge I see the 'less than' specifier is basically going to kill people's software in 2 years.
        - Marianne: An other way to put this is that "0.19.X" is not a sustainable choice.
    - Mark:
        - Detecting `pip` vs `conda`, different installers will have different requirements.
    - Mark: Should the migration guide should include best practices for: debian? red-hat?
        - Ubuntu 21.04 I can install scikit-image 0.18.1
        - `@olebole` packages scikit-image quite quickly for "debian"
            - Which version do we recommend that they use?
            - Example of packaging issues they raise:
                - https://github.com/scikit-image/scikit-image/issues/4366
            - They reaised issues about the dynamically downloaded files that we had to move out of the repo due to size.
    - Mark:
        - Can we create `from skimage.v0 import X` to allow people to stick to the old version without warnings?
        - Marianne: isn't this `skimage1` and `skimage2` proposal?
            - Mark: I don't think so, since it is the same package. 
                - We only have to maintain 1 infrastructure. 
                - We can copy all the tests over, and ensure that they continue to work.
            - Marianne: don't we have to deal with breaking changes?
                - Can we can slow down functions? Maybe we can guarantee correctness, but not performance for `skimage.v0`.
            - Marianne: The change with `preserve_range` in Gaussian and other filters is not just performance, it's breaking. 
    - Mark: Is there an option for writing code that works for V1.0 and V0.19?
        - Ideal: find the scale of the impact of scikit-image https://github.com/mamba-org/mamba 
    - Marianne: Parallel between **Python2 to Python3**
        - Unicode literals were a game changer in the migration. People were able to write "python 3 style" but users of python 2 were able to use the code too.
        - Numpy had `numpy.compat` for a VERY long time.
            - They still do, due to the fact that things change within python 3.5 -> 3.6 ... -> 3.9.

    - Mark: ideas:
        - Crawl through pypi and identify all dependencies on skimage.
        - Crawl through conda and identify all dependencies on skimage
        - Marianne: see https://github.com/scikit-image/boilerplate-utils/pull/4

    - Who should use 0.19.0?
        - People that don't depend on skimage in **their** code
            - Consider users of a package like https://cellprofiler.org/
            - They would want to use 0.19.0 while cellprofiler updates.
        - Researchers running Jupyter notebooks with results published within 2 years.
    - Who should use 0.20.0?
        - Maintainers of https://cellprofiler.org/
        - People who have CI system infrastructure?
    - Scikit-image user story:
        - Mark: We maintain a package that depends on scikit-image.
            - Do we use the new 1.0 API?
            - Do we stay with the 0.19 API?
        - Mark: Honestly, I don't care, whatever my **users** want. I don't drive this decision.
            - I need to be compatible with both.
        - Personal solution:
            - We (Mark's company) would be forced to create a compatiblity layer.
            - We (Mark's company) would be forced to reconsider the scikit-image dependency <--- this is a problem for scikit-image

## immediate todos

- review/approve/merge https://github.com/scikit-image/scikit-image/pull/5444
- random number generator always uses unified API. https://github.com/scikit-image/scikit-image/issues/5357 Some bits were missing from that PR (use `git grep` to find them). Nice place to unify `random_seed=` or `random_state=` keyword.
- review/approve/merge https://github.com/scikit-image/scikit-image/pull/4482
- Juan: finish RAG migration from skimage.future.
