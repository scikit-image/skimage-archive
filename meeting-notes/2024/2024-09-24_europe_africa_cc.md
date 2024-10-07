# scikit-image Community Call

- **Time:** Tue, 2024-09-24, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Marianne, Michael, Lars

## Agenda

- [[0.23.2] test_active_contour_model.py fails on mips64el #7425](https://github.com/scikit-image/scikit-image/issues/7425)
  - Do we support mips64el or do we just close this?
    - S: historically: we are very willing to merge patches (provided by, e.g., Debian), but we don't directly test on / support those systems

- Apply to [NIH RFA-OD-24-010 grant](https://grants.nih.gov/grants/guide/rfa-files/RFA-OD-24-010.html) for scikit-image?
  - Letter of intent: December 4 minus 30 days
  - Submission: December 4, 2024 (earliest submission Nov 4th)
  - Stéfan is planning to form a team to submit on behalf of skimage, with Berkeley as "host" institution; please let him know if you are interested

- docstub progress https://github.com/scientific-python/docstub
  - https://github.com/scikit-image/scikit-image/pull/7546


- **Review coordination**
  - [Improve stability of local_minima #7534](https://github.com/scikit-image/scikit-image/pull/7534), waiting for 2nd approval
  - [Render paragraphs in dormant message #7549](https://github.com/scikit-image/scikit-image/pull/7549), minor tweak
  - Anything else...?
