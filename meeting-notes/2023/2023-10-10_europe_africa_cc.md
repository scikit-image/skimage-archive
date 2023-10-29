# scikit-image Community Call

- **Time:** Tuesday, October 10, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Egor, Jarrod, Stéfan, Lars

**Moderator:**

## Agenda

- [Web analytics for scikit-image](https://views.scientific-python.org/scikit-image.org) works great (thanks to Scientific Python!)
  - Who want's access? Should we just make it public to everyone?
  - How hard is it to get [Google Search integration](https://plausible.io/docs/self-hosting-configuration#google-search-integration) working?
    - Added [scikit-image Search Console](https://search.google.com/search-console/users?resource_id=sc-domain%3Ascikit-image.org), albeit without the click-through button integration. 
    - Currently access given to Jarrod, Egor, Lars, Stéfan
- Waiting for PyWavelets release to support Python 3.12
- 0.23 slated for ~January
	- Can we get more features in this time around?
		- [Chris Luengo's morphology improvements](https://github.com/scikit-image/scikit-image/pull/6695)
		- [Thin plate splines](https://github.com/scikit-image/scikit-image/pull/7040)
			- Loop back on the [original image.sc discussion](https://forum.image.sc/t/equivalent-for-matlabs-piecewiselineartransformation2d/51035)
		- [Haussdorf improvements](https://github.com/scikit-image/scikit-image/pull/6914)
		- Egor is looking into [medial axis in 3D](https://github.com/scikit-image/scikit-image/issues/4105), perhaps for 0.24
		- Maybe: [Add function to remove near objects in nd-image](https://github.com/scikit-image/scikit-image/pull/4165)
- Typing support
	- Community summit?
	- Need to type things like Image, Mask while still allowing NDArray as input
	- See [discussion on typing in #7191](https://github.com/scikit-image/scikit-image/pull/7191#issuecomment-1769725099)
	- [PEP646](https://peps.python.org/pep-0646/) [support in mypy was completed](https://github.com/python/mypy/pull/16242)
- Discussion around skimage2
  - There are opportunities for normal deprecations on [API changes for skimage2](https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2), just grab a few & clean up list


## [Previous meeting (2023-09-26)](https://github.com/scikit-image/skimage-archive/pull/50)

**Present:** Biola, Lars, Marianne, Stéfan

- Question when updating dev env:
    - [Update section](https://scikit-image.org/docs/stable/user_guide/install.html#updating-the-installation) needs updating.
    - `spin build` accepts a `--clean` option that removes `build-install`
- Web analytics in our docs
  - https://github.com/scikit-image/scikit-image/pull/7145 got merged
  - Login on https://views.scientific-python.org/login
    - Lars: didn't receive login information yet?
    	- Sent via email to Lars & Marianne, admins that can add others
- How to use the `skimage2` milestone?
    - e.g., can I just add it to https://github.com/scikit-image/scikit-image/issues/7117#issuecomment-1735939832?
  - [API Changes for `skimage2`](https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2) (wiki)
    - [Discussion issue](https://github.com/scikit-image/scikit-image/issues/5439)
- Release: [waiting on pywt](https://github.com/PyWavelets/pywt/pull/687#issuecomment-1735511302)
  - Make pywt an optional dependency. It's only used in one module`_denoise.py`
  - Lars will make a PR
- [0.22 milestone](https://github.com/scikit-image/scikit-image/milestone/25)
- [EOSS 6](https://chanzuckerberg.com/rfa/essential-open-source-software-for-science/)
  - Lars has until January 2025 on current grant
  - [CZI Data Insights Cycle 3 (Single Cell)](https://chanzuckerberg.com/rfa/single-cell-data-insights/)
  - Marianne will reach out to potential collaborator on CZI LoIT
  - **DEADLINE:** October 17th


-------------------------------------------------

**After the meeting**, please commit the notes to our [scikit-image/skimage-archive](https://github.com/scikit-image/skimage-archive) repository.
