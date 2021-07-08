# skimage 1.0 API changes notes

[Meta-issue](https://github.com/scikit-image/scikit-image/issues/5439)

## 1. Europe/Asia

Present: Marianne, Juan

Meeting date: 2021-07-01 at 10:00 CEST

- Juan likes Marianne's proposal to add `channel_axis` to functions that assume final channel axis: https://github.com/scikit-image/scikit-image/issues/5439#issuecomment-867547754

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
        - Ubuntu 21.04 I can install Scikit-image 0.18.1
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

## 3. US/Pacific — jul 07, 2021

Present: Greg, Stéfan, Juan, Mark, Alex

* Module deprecations

  - `skimage.viewer`: consensus on call that it should be deprecated
    - tutorial examples should be ported to Napari (magicGUI) or matplotlib
    - can improve deprecation warnings: docstring in module, warning when importing module
  - imageio:
      - ImageCollectionReader: useful to process 2k files. You can instantiate the collection without any cost.
          - Handles wildcard.
          - You can change caching to be on or off.
      - Juan:
          - It is quite complex, and the issue with multiple 
      - Look at if imageio bundles tiffile and if they have an ancient version.
          - tifffile has become SO MUCH easier.
          - They do seem to bundling the version from 2018
              - https://github.com/imageio/imageio/blob/master/imageio/plugins/_tifffile.py#L78
              - https://github.com/imageio/imageio/issues/437
          - Push for just using tifffile straight. It is a pure python dependency that just depends on numpy as of recent versions.
      - imageio should not be optional.
      - Should ensure that we depend on the most important imageio plugins.

* Function / module moves
  - RAG:
      - Juan stalled moving it out of `future`. And realized that there was a bug, and maybe there is a BUG?
  - Getting rid of future?
      - Stefan: Things seem to get stuck a little bit.
      - Juan: they don't have to.
          - If we want to get rid of deprecations and become fully stable, then future is the only place where we can be stable.
      - Stefan: the intent is to move things from future to stable.
      - Maybe consider renaming it `experimental`?

* Parameter removal
  - Removing `preserve_range`:
      - Some code bases have it, and some will not be using it.
      - A 6 version transition to remove the parameter.
          - Currently the default is False. Need to make it True, so we need to give warnings.
          - Then removing it will take 2 remove it.
      - It will be noisy forever if we take the standard deprecation cycle.
      - A global switch is probably ok, but not OK.
      - Tensorflow did compat.v1 the problem, we would be dragging the newer version and we would have some problems.
          - How would the previous code interact with the newer code?
          - We would have double the API.
          - Juan: maybe we don't, maybe it is a complete silo.
              - People can do skimage.v0.alskdjf
              - And people can migrate at their own pace.
      - How is this going to work with matplotlib?
          - Currently, the problem is that RGB images fail when they aren't between `[0, 1]`.
          - Tom was willing to move forward.
          - Generally, performance optimizations can be explained in a migration guide.
      - How to save floating point images between `[0., 255.]`
          - If the plugin requries uint8 then it will be seamless.
          - Ask users to manually rescale.
      - A link to a transition guide is nice.
          - Maybe link to GitHub issue / discussion / **wiki** page?
          - Mark introduced a parameter `_stacklevelincrement` can be used to have the caller control wher ethe warning appears.
      - Related transpositing coordinates is super slow if we try to go the
      - Mark; If the problem gets big enough, then we will create `skimage_compat.v0` and `skimage_compat.v1` ourselves
      - Stefan: how big of a pain was the LTS?
          - Juan thought it was not so horrible???
          - Maybe do v0.19 
          - Mark: thinks it was alot of work.
              - But maybe not as bad all in all.
  - Juan:
      - Write a SKIP for one shot API changes for reaching out to the broader community.
      - General idea:
          - Release 0.19 "LTS"
              - Release notes should explain 0.20 scheme, upcoming change in API,  and suggest pinning
              - Documentation for 1.0 should also emphasize the API change
              - Website should advertise 1.0 API change
          - Release 0.20, same as 0.20 but with a big giant warning to pin.
              - Released day after 0.19.
                - Warns to pin to `!=0.19`
                    - Should we use a print statement instead of a warning to ensure it appears?
                    - We should ensure that we don't print when the ``stdout`` doesn't exist.
                        - S: We have a custom warning class; think we can force that to always appear (will appear at least once?)
                - 0.19 does not receive updates; should be made clear to users
                - Make clear to distributions *not* to package this version
              - Point to the migration guide? (yes, in both releases)
              - Stefan:
                  - Do we backport bugfixes here?
                  - Juan: maybe, but seems to have minimal value.
          - Release 1.0.0.rcX frequently?
          - Release 1.0 when we are ready.
      - Alex:
          - We are catering after 5 different groups.
          - Very likely many of these people will be using scikit-image 1.0.
          - Maybe we don't 
      - Mark:
          - Can we add a decorator ``@parameter_removed("1.0", "preserve_range")``
              - We have something similar for deprecations
          - And link to the migration guide? EVERYWHERE
      - migration guide:
          - General Migration Guide Issue:
          - discussion: Targetted issue
          - Doc page (a bit tricky with getting the URL ahead of time---point to dev, or released ver? can be auto-generated with a function that looks at `__version__`)
              - We do have these permenant page?
              - We can upgrade webpages to build markdown.
          - Github **wiki** page
              - Mark likes this
              - S: could work fine, we just need a standard "url scheme"
  - Stefan:
      - Can we bundle a few API changes?
      - Juan: Yes the goal is the bundle all API changes into 1.

* Extra information API discussion needs to happen at some point

- NumPy vs. SciPy vs. ¡scikit-learn! ¡tensorflow! ¡pytorch!
    - Boundary modes: for 1.0 we could consider matching ndimage instead of NumPy
    - Parallel: workers/n_cpus/n_jobs/processes
    - Mark: is this really important, at one point just: RTM (Read The Manual)
    - For some of these, we should coordinate with the community (see [SPECS](https://scientific-python.org/specs/))

* Parameter/function renaming
 - Alex does not like "segmentation" for labels
 - S: agreed, labels are pretty widely understood, and segmentation seem more topic-specific

* Protocols
  - [PEP 544](https://www.python.org/dev/peps/pep-0544/)
  - Should we group functions according to protocol?
    `skimage.filters.threshold.*`
    `skimage.filters.*other random funcs*
  - A bigger transition than most others discussed so far; will require fairly incisive search/replacing to upgrade

* Metadata
  - Structured logging mechanism
    ```python
    log = skimage.log()
    
    out = any_function(*args, **kwargs)
    extra = log[-1]
    ```
  - `out, extra = any_function(*args, **kwargs)` with `extra` being a dictionary (whose keys we can type)
  - `out, extra = any_function.extra(*args, **kwargs)` vs `out = any_function(*args, **kwargs)` (Gaël offers to say "no" to that); it does feel a bit magical and definitely not common
  - `out, extra = extra(any_function)(*args, **kwargs)`
  - `out, extra = extra.any_function(*args, **kwargs)`
  - `out, extra = any_function_extra(*args, **kwargs)`
  - S: [Doable with typing, btw](https://docs.python.org/3/library/typing.html#typing.overload):
  - `out, extra = any_function(*args, **kwargs, extra=True)`
  - `out = any_function(*args, **kwargs, extra=False)` <- default
  - `extra` should always be the same object (dict, bundle, whatever)

## immediate todos

- Juan: review/approve/merge https://github.com/scikit-image/scikit-image/pull/5444
- random number generator always uses unified API. https://github.com/scikit-image/scikit-image/issues/5357 Some bits were missing from that PR (use `git grep` to find them). Nice place to unify `random_seed=` or `random_state=` keyword. Greg recently opened a PR with some additional random API cleanup (but no parameter renaming): https://github.com/scikit-image/scikit-image/pull/5450
- review/approve/merge https://github.com/scikit-image/scikit-image/pull/4482
- Juan: finish RAG migration from skimage.future.
- Deprecate viewer module, not just ImageViewer class
- Mark: Push for tifffile dependency update in imageio
- Juan: Add notes to release instructions about reviewing skimage.future
- Border mode can be matched to ndimage in 1.0 instead of numpy.pad
- Mark: Make/tag issue about pooch creating a data dir on import
