# scikit-image Community Call

- **Time:** Tue, 2024-12-17, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Michael Bratsch, Lars Grüter, Aditi Juneja, Jarrod Millman, Stéfan van der Walt

## Agenda

- Fixes for [0.25.1](https://github.com/scikit-image/scikit-image/milestone/31) patch release
  - [Gallery example on morphological snakes uses removed attribute 'collections.' #7636](https://github.com/scikit-image/scikit-image/issues/7636)
    - Fix: [Don't use removed QuadContourSet.collections in gallery example #7638](https://github.com/scikit-image/scikit-image/pull/7638)
  - New sparse related failing tests reported by Debian:
    [[0.25.0] test_random_walker.py tests fail with float16 #7635](https://github.com/scikit-image/scikit-image/issues/7635)
    Dan is taking a look

- [Blur effect fix](https://github.com/scikit-image/scikit-image/pull/7598)

- [Use pytest config in pyproject.toml in CI #7555](https://github.com/scikit-image/scikit-image/pull/7555)

- How to catch deprecation warnings in sphinx-gallery in-time?

- How to skip slow gallery examples if desired

- Aditi's dispatching SDG 🎉
  - Contract until March 19
  - Next steps?
    - Get in the prototype - [PR#7520](https://github.com/scikit-image/scikit-image/pull/7520)
    - expand on the `BackendInformation` and backend metadata handling - coordinate with @betatim on this ([#7550](https://github.com/scikit-image/scikit-image/issues/7550))
    - [TODO:Aditi] better handling of type-based dispatching (or backend specific dispatching)
    - exploring ways of testing the dispatching mechanism
    - enabling automatic testing for backends
    - Later-- coordinate with `cuCIM` people to setup `cuCIM` as a backend package.
