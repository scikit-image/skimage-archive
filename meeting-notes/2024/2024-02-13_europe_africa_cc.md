# scikit-image Community Call

- **Time:** Tuesday, February 13, 2024, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- **Notes:** https://hackmd.io/@lagru/HJDpuhEvB/edit
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Lars

## Agenda

- NumPy 2
  - [Test nightly wheel build with NumPy 2.0 #7288](https://github.com/scikit-image/scikit-image/pull/7288)
  - Nearly done, only some dtype shenanigans in SIFT missing
  - Keeping `lookfor` vendored in scikit-image (`numpydoc` would pull in sphinx)
- [SciPy 2024 Tutorial](https://discuss.scientific-python.org/t/tutorial-at-scipy2024/969)
  - Discussed inviting some newcomers
- [Create SECURITY.md #7230](https://github.com/scikit-image/scikit-image/pull/7230)
  - Lars will sign up as co-lifter
- [Josh's post](https://discuss.scientific-python.org/t/possible-alternative-path-to-skimage2-adapt-the-matplotlib-rcparams-infrastructure/952/3) re matplotlib.rcParams structure instead of skimage2
