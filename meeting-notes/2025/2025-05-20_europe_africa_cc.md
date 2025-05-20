# scikit-image Community Call

- **Time:** Tue, 2025-05-20, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Lars

## Agenda (2025-05-20)

- [Add preserve_range parameter to `feature.blob_*` functions #7797](https://github.com/scikit-image/scikit-image/pull/7797)
- Exposure to JasonEtco/create-an-issue in our release workflow?
  See [#7787 (comment)](https://github.com/scikit-image/scikit-image/pull/7787#discussion_r2086898797)
  - Probably OK, since it runs only on failure; if that action *specifically* targeted skimage, they could upload a fake wheel
    if they could somehow get hold of credentials?
  - Why are standard actions, like for making issues, not a GH action?
  - Should we only use actions from trusted orgs? E.g., scikit-learn, scientific-python, etc.?
    - A good goal to work towards in the long run. Unless action updates by DependaBot are code reviewed,
      we are not safeguarded against malicious changes.
  - https://github.com/thomasjpfan/labeler
  - Existing allowed actions: https://github.com/scikit-image/scikit-image/settings/actions
    - Current external orgs:
      - astral-sh
      - docker
      - mymindstorm
      - scientific-python
      - deadsnakes
      - prefix-dev
      - jasonetco
      - conda-incubator
      - pypa
- Merge migration guide so we can modify it in PRs
- [CI efficiency PR](https://github.com/scikit-image/scikit-image/pull/7749)
- Brief discussion on docstub and overloading
