# scikit-image Community Call

- **Time:** Tuesday, July 2, 2024, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Lars, Marianne, Josh

## Agenda

- Discussed spin: It's just a 'normal' dependency (i.e., will get its new features when we update its version, cf. https://github.com/scikit-image/scikit-image/blob/bbf94f879ffe197f96305c37593a86b43206b4c9/requirements/build.txt#L11).
- Marianne: create issue at https://github.com/dask/dask about imread relying on our ski.io.imread
- Joined [skimage/napari tutorial](https://cfp.scipy.org/2024/talk/PQMQ3K/) at SciPy 2024 next week
  - Prepping https://github.com/scipy-2024-image-analysis/tutorial
  - Look for issues/PRs/topics for a potential sprint!
    - Update outdated import patterns for skimage to the lazy-loading based approach
- [EuroSciPy 2024](https://euroscipy.org/2024/)
  - skimage tutorial, need more presenters
  - Marianne has an accepted talk!
  - Coordination around skimage at EuroSciPy
    - poll whether to do skimage sprint before or after conference
    - book shared AirBnB or similar for all skimage maintainers?
- [Affine registration #7421](https://github.com/scikit-image/scikit-image/pull/7421)
  - Follow-up of [Affine Image Registration #3544](https://github.com/scikit-image/scikit-image/pull/3544)
- Fixing CI
  - [pre-commit autoupdate #7452](https://github.com/scikit-image/scikit-image/pull/7452)
  - [Test_remove_near_objects fails on i386 (0.24.0) #7450](https://github.com/scikit-image/scikit-image/issues/7450)
