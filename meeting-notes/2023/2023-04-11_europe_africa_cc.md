# scikit-image Community Call

- **Time:** Tuesday, Apr 11, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Jarrod, Stéfan, Lars

**Moderator:** -


## Agenda

- scikit-image v0.21
  - [0.21 milestone](https://github.com/scikit-image/scikit-image/milestone/9): ~42 open
  - Schedule: rc0 on April 11, final on April 14
  - Do something about [PermissionError when creating data_dir when user doesn't have permissions #4664](https://github.com/scikit-image/scikit-image/issues/4664)
- Discussion around how we use milestones in our workflow
  - Stéfan & Lars use it to priortize items
  - Not every item on this list is required or should block a release. Rather, it's fine to postpone or remove them from the list as long as a core developer re-evaluates the current priority.
  - Every merged PR should go into the appropriate milestone for the pending release.
- Policy for private modules
  - With lazy loading it's now harder to discover private API
  - But, we should still be consistent, and the `_` is a very clear signal that a sub-submodule is private
  - Will do a one-shot renaming of all sub-submodules
  	- Also add note in the contributor guide
- Outreachy
  - Candidates have been rated.
  - We have funding for two, with three potential candidates.
  - Friday is intern selection deadline.
- EOSS3 report
  - Greg working on report, NumFOCUS will do financial report.
