# scikit-image Community Call

- **Time:** Tuesday, Apr 18, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Jarrod, Lars, Stéfan

**Moderator:** -


## Agenda

- skimage v0.21
	- Have to resolve random API
		- [commented on SciPy PR](https://github.com/scipy/scipy/issues/14322#issuecomment-1513911293)
		- We're going to hold off on the release for a few days to see if we can get this resolved.
	- Issues that need fixing:
	  - Docs directory needs cleaning (remove unnecessary files, simplify hierarchy / update Makefile)
	  - `RELEASE.txt` is outdated
	  - No API changes/deprecations were documented during development :scream:
	  - Simplify release notes (too much manual work required)
	  - Release notes script does not generate the output format we use and needs better error message
	  - PR template is way too long and gets ignored; edit down and include the basics (such as checking for / documenting API changes!)

- skimage v2
	- The scope is very large at the moment. Therefore:
		- Who is going to do all that work?
		- Need to prioritize needed changes.
		- [Concern](https://discuss.scientific-python.org/t/project-continuity-skip-4/665/3?u=stefanv)
