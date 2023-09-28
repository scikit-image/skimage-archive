# scikit-image Community Call

- **Time:** Tuesday, September 26, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Biola, Lars, Marianne, Stéfan

## Agenda

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
  - Marianne will reach out to potential collaborator on CZI LOI
  - **DEADLINE:** October 17th
