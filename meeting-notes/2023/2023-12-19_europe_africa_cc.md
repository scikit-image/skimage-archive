# scikit-image Community Call

- **Time:** Tuesday, December 19, 2023, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://framatalk.org/skimage-community)**
<!-- - **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)** -->
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

## Agenda

**Present:** Lars, Stéfan, Biola, Marianne

- [Build package for Pyodide out of tree #7265](https://github.com/scikit-image/scikit-image/pull/7265) currently blocked by [build error](https://github.com/scikit-image/scikit-image/actions/runs/7180894298/job/19554131919#step:6:92)
  ```
   #error "LONG_BIT definition appears wrong for platform (bad gcc/glibc config?)."
  ```
	- [Can build locally](https://pyodide.org/en/stable/development/building-and-testing-packages.html)
- Requested PRs waiting for review:
  - [Add thin-plate splines warping #7040](https://github.com/scikit-image/scikit-image/pull/7040)
      - Marianne will review by tomorrow
  - [Test building nightly wheels with nightly NumPy 2.0 #7251](https://github.com/scikit-image/scikit-image/pull/7251)
  	- Approved; will merge on green
- skimage2
  - Currently under review / iteration: [Add new deprecate_parameter helper #7256](https://github.com/scikit-image/scikit-image/pull/7256)
    - blocks: [#7225](https://github.com/scikit-image/scikit-image/pull/7225), [#7255](https://github.com/scikit-image/scikit-image/pull/7255)
- Typing stubs (Lars)
  - Plan is to type public API and type check only tests for a start
  - Slow going, struggling a bit with configuration that allows for incrementally adding stubs
- Low hanging fruits
  - [Describe rotation as counter-clockwise in projective transforms #7031](https://github.com/scikit-image/scikit-image/pull/7031)
  	- Need to [investigate futher](https://github.com/scikit-image/scikit-image/pull/7031#issuecomment-1863238694): looks like `ski.transform.warp` does not handle inverse tf the way it should?
  	- Small bug in docstring of warp: "images" instead of "image"
  - [Rework docstring of ImageCollection #6988](https://github.com/scikit-image/scikit-image/pull/6988)
