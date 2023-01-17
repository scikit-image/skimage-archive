# scikit-image Community Call

- **Time:** Tuesday, January 17, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Marianne, Lars, Stéfan

**Moderator:** -

## Agenda

- [HackMD doc by Scientific Python](https://hackmd.io/@scientific-python/HJWUBDVNi) is readonly?
	- Message "Sorry, this team is disabled. You can't edit this note."
	- HackMD agreed to upgrade our account again; Stéfan emailed them to find out when this will happen
- Respond to [New (experimental) type stubs for skimage](https://discuss.scientific-python.org/t/621)
	- One of the goals of the CZI5 grant is to add type annotations to scikit-image
	- might be a useful starting point / reference to keep in mind
- Release 0.20
	- Blocked by [Build wheels for arm64 on macos
#6667](https://github.com/scikit-image/scikit-image/issues/6667) -> [seems to work now!](https://github.com/scikit-image/scikit-image/issues/6667#issuecomment-1385737507)
	- [0.20 milestone](https://github.com/scikit-image/scikit-image/milestone/22), ~16 open items
- Talked about some growing pains with meson-python, e.g. [meson python editable install issues](https://github.com/mesonbuild/meson-python/issues/47#issuecomment-1377181559)
- Documentation on setting up a dev environment is broken / inconsistent
	- pip & conda use different version specification syntaxes
	- packages may be named differently on PyPI and conda-forge
	- See https://github.com/scikit-image/scikit-image/issues/6494#issuecomment-1385695486
	- CI should test dev environment setup
- Revise our HTML documentation
	- Use pydata-sphinx-theme, e.g. [networkx also uses a gallery](https://networkx.org/documentation/stable/auto_examples/index.html)
	- Lars intends to prepare a draft PR
- Logo redesign, see https://discuss.scientific-python.org/t/536
