# scikit-image Community Call

- **Time:** Tuesday, May 31, 2023, 19:00 – 20:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Jarrod, Lars, Stéfan

**Moderator:**

## Agenda

- Release v0.21
  - Don't test numpy nightlies due to transcendental functions issue https://github.com/scikit-image/scikit-image/pull/6973
  - Don't highlight the JupyterLite as we are reverting it temporarily for v0.21 https://github.com/scikit-image/scikit-image/pull/6972 -> removed highlight label from https://github.com/scikit-image/scikit-image/pull/6911
  - Update release notes https://github.com/scikit-image/scikit-image/pull/6949
- Updating eagle.png broke v0.19
  - Which solution should we take? Revert or create patch release https://gitlab.com/scikit-image/data/-/merge_requests/22#note_1413062475
