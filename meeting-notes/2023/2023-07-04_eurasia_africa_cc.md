# scikit-image Community Call

- **Time:** Tuesday, July 04, 2023, 17:00 – 17:45 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Lars, Marianne 

**Moderator:**

## Agenda

- [Joint tutorial with Napari at SciPy 2023 next week](https://cfp.scipy.org/2023/talk/NEUUKG/)
- Endorsing SPECs:
  - wheels testing and uploading
  - deprecation policy
  - formalized practices already in use
  - https://github.com/scientific-python/specs
- [Clarify objection period for lazy consensus in SKIP 1](https://github.com/scikit-image/scikit-image/pull/7020)
  - Opinions on the recommended lengths of objection periods?
      - Marianne: +1 for durations recommended by Egor; -1 on automated merging.
- [Inpainting example (Outreachy)](https://github.com/scikit-image/scikit-image/pull/6853#issuecomment-1597508878) ready for final round of reviews!
- [TPS warping (Outreachy)](https://github.com/scikit-image/scikit-image/pull/7011)
  - Clarification for plans in this [comment (#2429)](https://github.com/scikit-image/scikit-image/issues/2429#issuecomment-816404636)
    - "solve the linear equations directly"?
    - "redo the low-res transformation"? -> `scipy.ndimage.map_coordinates`
- Automatic changelog generation: https://github.com/scientific-python/changelist
