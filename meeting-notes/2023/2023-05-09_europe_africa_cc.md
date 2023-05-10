# scikit-image Community Call

- **Time:** Tuesday, May 9, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:**  Jarrod Millman, Stéfan van der Walt, Lars Grüter

**Moderator:** -

## Agenda

- skimage v0.21 waiting for random seeding PR (rename "seed" to "rng")
- PRs for attention:
  - [10x speed up for transform.PiecewiseAffineTransform](https://github.com/scikit-image/scikit-image/issues/6864)
  - [Add ignore errors to regionprops table](https://github.com/scikit-image/scikit-image/issues/6603)
  - [faster conversion between RGB and HSV colorspaces](https://github.com/scikit-image/scikit-image/pull/5362)
  - [Use imageio v3 API](https://github.com/scikit-image/scikit-image/pull/6764)
  	- Merged data update on gitlab. Lars will push new data hash to PR.
- [User question re bounding box + area](https://forum.image.sc/t/how-i-get-area-and-box-easily-from-scikit-image-contour/80452/)
- pre-commit bot: https://discuss.scientific-python.org/t/scikit-image-community-call-announcements/527/39
- Two outreachy interns accepted!

## Previous agenda (2023-05-03)

- skimage v0.21
  - Resolve the Random API
    - Stéfan: [Wrote a SPEC](https://github.com/scientific-python/specs/pull/180)
    - Stéfan: [I propose that we switch to `rng` instead of `seed`](https://github.com/scientific-python/specs/pull/180#issuecomment-1532266050)
    - Stéfan: For those who enjoy [long background discussions](https://github.com/scipy/scipy/issues/14322)
