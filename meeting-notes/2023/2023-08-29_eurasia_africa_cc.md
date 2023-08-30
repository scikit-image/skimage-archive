# scikit-image Community Call

- **Time:** Tuesday, August 29, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Juan Nunez-Iglesias, Egor Panfilov, Lars Grüter, Adeyemi Biola

**Moderator:**

## Agenda

- Lighting talk at NumFOCUS summit?
  - Lars: Perhaps on skimage2 transistion to collect further insights and feedback from the community
- Juan: other topics to discuss at NumFOCUS summit:
  - typing issues re protocols for functions (the **kwargs problem)
    - super half baked idea: can we wrap a full signature into a compliant signature using **kwargs, or vice versa?
  - fundraising
- Egor:
  - wants to catch up on a few bigger discussion - https://discuss.scientific-python.org/t/a-pragmatic-pathway-towards-skimage2/530
  - discuss at the Summit - usage analytics
  - medial axis 3D - eventually to be a PR
  - local thickness - within the scope of scikit-image, to be a PR
- Pytest config
  - [Update pytest config in pyproject.toml with repo-review recommendations #7063](https://github.com/scikit-image/scikit-image/pull/7063)
  - Lars: move [custom warning filter configuration](https://github.com/scikit-image/scikit-image/pull/7063#discussion_r1288429465) to pytest config
- Ready to merge, smallish
  - [Include skimage.morphology.skeletonize_2d in our public API and doc #7094](https://github.com/scikit-image/scikit-image/pull/7094)
  - [Avoid unnecessary padding in skimage.measure.block_resize #7092](https://github.com/scikit-image/scikit-image/pull/7092)
  - [For uniform intensity images, return intensity value as threshold
 #7098](https://github.com/scikit-image/scikit-image/pull/7098)
