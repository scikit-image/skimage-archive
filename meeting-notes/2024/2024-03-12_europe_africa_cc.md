# scikit-image Community Call

- **Time:** Tuesday, March 12, 2024, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Lars

## Agenda

- [CI jobs with optional dependencies are failing #7339](https://github.com/scikit-image/scikit-image/issues/7339)
  - [Possible fix #7340](https://github.com/scikit-image/scikit-image/pull/7340)
- Plugin's in `skimage.io`
  - Is `imread` plugin still relevant? 
    https://pypi.org/project/imread/ is no longer a dependency
  - Same with `osgeo.gdal`
  - I suspect nose style `setup` and `teardown` have broken for some time now ([deprecated by pytest](https://docs.pytest.org/en/latest/changelog.html#id179))
    We need to clean that up ASAP
  - For 2.0, remove plugin infrastructure, support thin interface around `imageio`; users should simply bring their own NumPy arrays. We can document libraries like [fits](https://docs.astropy.org/en/stable/io/fits/index.html), etc.
  	- `imageio` has its own plugin system.
- NumPy 2.0 release candidate is out
  - Nightly job is broken, possibly due to NumPy 2.1.0?
  - still pending [Follow-up cleaning & fixes for compatibility with NumPy 1 & 2 #7326](https://github.com/scikit-image/scikit-image/pull/7326)
  - To build wheels, we'd need to install NumPy 2 from the pre-release channel
- SciPy2024 tutorial proposal has been submitted
