# scikit-image Community Call

- **Time:** Tue, 2025-03-11, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**


## Agenda

**Present:** Lars, Matthew, Stéfan, Aditi

- [#7739](https://github.com/scikit-image/scikit-image/pull/7739): `remove_small_objects`. Should be close to merge, only a few docstring tweaks left.
- How to deal with `img_as_` functions 
	- [Lars' comment](https://github.com/scikit-image/scikit-image/issues/1234#issuecomment-2714385294)
	- Can raise when `preserve_range` is not set in individual functions
	  - In skimage2, can just swallow `preserve_range=True`
	  - By doing `import skimage2`, user acknowledges the no scaling approach
- `dimensions` in transformation `__init__`
  - Currently, transforms always take dimensionality, but really we should not have two ways of specifying it. It should either be inferred from coordinates or matrix, or be specified explicitly for empty transform.
  - Want to move to `Transform.identity(dimensions=3)` or similar for latter case
  - What about `scale=2` case? Could apply equally to 2D, 3D; Matthew chose: `scale=(2, 2, 2)`?
    - What about `scale=5` Then we get 2D transform (default dimensionality still 2).
    - Only case that will break right now is `(scale=2, dimensionality=3)`
      - The new rule is "dimensionality has to be derived from model arguments"
      - Becomes `(scale=(2, 2, 2))`
- [Affine registration #7421](https://github.com/scikit-image/scikit-image/pull/7421)
  [ECC algorithm Zulip thread](https://skimage.zulipchat.com/#narrow/channel/181448-development/topic/ecc.20algorithm.20based.20on.20PR.20.237050)
  [Loïc's PR #7666](https://github.com/scikit-image/scikit-image/pull/7666)
