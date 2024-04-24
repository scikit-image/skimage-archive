# scikit-image Community Call

- **Time:** Tuesday, April 23, 2024, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Marianne, Adeyemi, Lars

[Reviewed by Stéfan/Lars afterwards]

## Agenda

### Conferences

- [Tutorial for SciPy 2024](https://cfp.scipy.org/2024/talk/review/WG79CZFKBRAAWQCRCANTXE7ABVMWUSDC) was accepted
  - Iteration of previous year's tutorial will happen in [scipy-2024-image-analysis/tutorial](https://github.com/scipy-2024-image-analysis/tutorial)
  - Do we know who will be there (definitely)?
  - How do we get Adeyemi there?
- [EuroSciPy 2024](https://euroscipy.org/2024/) announced on Aug. 26 - Aug. 30, 2024 in Szczecin, Poland
  - The idea was to do a skimage sprint there and get all maintainers together with EOSS5 funding.
  - Who can make it? (Lars, Marianne)
  - Marianne: will share ideas / draft on a talk on the forum


### EOSS5

- Path to skimage2
  - Ready to merge [Standardize function signature of compare_images #7322](https://github.com/scikit-image/scikit-image/pull/7322)
  - [skimage 2 timeline](https://hackmd.io/VDEX5MLWQPaP-ImxYx8uWA): Last release with old API / feature freeze [in May](https://hackmd.io/VDEX5MLWQPaP-ImxYx8uWA#2024-5-Last-release-with-old-API)!
    - Lars: start document listing concrete breaking changes, a "migration guide" to be so to speak
- Typing skimage
  - Juan & Lars discussed [docs2stubs](https://github.com/gramster/docs2stubs). The implementation has some limitations for what we are trying to achieve
  - Lars will re-assemble the tool for our use case with ecosystem in mind. E.g. use regex in mapping between docstrings and types
  - Stéfan suggests to define a grammar for parsers like [lark](https://lark-parser.readthedocs.io/en/latest/) instead of regex
- Outreachy: Lars to review and merge [Add thin-plate splines warping #7040](https://github.com/scikit-image/scikit-image/pull/7040) after meeting


### Other

- Reduce maintenance
  - Deprecate trivial inverse functions
    - [`local_minima`](https://scikit-image.org/docs/dev/api/skimage.morphology.html#skimage.morphology.local_minima), point to `local_maxima(-image, ...)`
    - [`remove_small_holes`](https://scikit-image.org/docs/dev/api/skimage.morphology.html#skimage.morphology.remove_small_holes), point to `remove_small_holes(~image, ...)`
      - would close [#4003](https://github.com/scikit-image/scikit-image/issues/4003) with very simple deprecation
    - Marianne & Stéfan are okay with this
  - Deprecate plugin infrastructure in `skimage.io` in favor of `imageio`
    - What's the scope of the deprecation?
    - Parameter `plugin` is used in old API and `imageio`, so pass-through would compete...
    - Marianne: It's not essentially our job to provide IO utilities (such as `imread` and `imsave`); it doesn't matter the IO library (imageio or other) as long as it returns a NumPy array, which can then be processed with scikit-image (Data Carpentry inspiration: IO vs image processing are two separate conceptual boxes).
    - Stéfan: imageio is not returning a "proper" array, would be good to keep a wrapper around that returns a pure NumPy array
- Not sure how to address [libatlas 3.10.3 related failures on debian](https://github.com/scikit-image/scikit-image/issues/7399)
  - How to debug other architectures locally?
- Tried out [pytest-randomly](https://github.com/pytest-dev/pytest-randomly) and it seems like we could do better with test independence...
