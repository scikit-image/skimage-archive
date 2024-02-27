# scikit-image Community Call

- **Time:** Tuesday, February 27, 2024, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- **Notes:** https://hackmd.io/@lagru/HJDpuhEvB/edit
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Marianne, Lars

## Agenda

- [🥾 Path to skimage2](https://github.com/scikit-image/scikit-image/labels/%3Ahiking_boot%3A%20Path%20to%20skimage2)
  - [Deprecate output and positional args in filters.gaussian #7225](https://github.com/scikit-image/scikit-image/pull/7225)
    waiting for review
  - [Deprecate function plot_matches in favor of plot_matched_features #7255](https://github.com/scikit-image/scikit-image/pull/7255)
    waiting for objection
  - [Use num_workers instead of alternate parameter names #7302](https://github.com/scikit-image/scikit-image/pull/7302)
    stalled, potentially resolved by SPEC
  - [Standardize function signature of compare_images. #7322](https://github.com/scikit-image/scikit-image/pull/7322)
- New features for next release
  - [Add thin-plate splines warping #7040](https://github.com/scikit-image/scikit-image/pull/7040)
    waiting for review
- Serious issues with current implementation of watershed algorithm?
    - [Fix watershed when markers aren't at minima #7071](https://github.com/scikit-image/scikit-image/pull/7071) under discussion
    - Closed issue about [default markers really being local minima or not #7117](https://github.com/scikit-image/scikit-image/issues/7117) (led to docstring update and raised a question of consistency: fix in skimage2?)
    - Gallery example [Segment human cells (in mitosis)](https://scikit-image.org/docs/stable/auto_examples/applications/plot_human_mitosis.html) uses watershed, which is supposed to further nuclei segmentation (i.e., increase the number of nuclei found), resolving cases of touching/overlapping nuclei, but the number of segmented nuclei goes from 288 to 286(?!); serious issue encountered when using the same technique for WIP gallery example with [embryo 3D data](https://github.com/scikit-image/scikit-image/pull/7309)
- [Discussion on SciPy 2024 tutorial](https://discuss.scientific-python.org/t/tutorial-at-scipy2024/969)
  - Who's joining from Napari's side
  - extended deadline Mar 5th AOE
- NumPy 2.0
  - We should be prepared
  - [Follow-up cleaning & fixes for compatibility with NumPy 1 & 2 #7326](https://github.com/scikit-image/scikit-image/pull/7326)
  - how close is their release candidate?
- Low-hanging fruits
  - [Don't use boolean shift as default in skimage.filters.rank functions #7320](https://github.com/scikit-image/scikit-image/pull/7320)
    (warn indefinitely or use deprecation?)
