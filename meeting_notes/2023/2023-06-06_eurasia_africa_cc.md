# scikit-image Community Call

- **Time:** Tuesday, June 6, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan van der Walt, Lars Grüter, Biola Adeyemi, Ananya Srivastava

**Moderator:**


## Agenda

- Announcing release v0.21
  - Lars: Scientific Python forum, image.sc, NumPy mailing list
  - Failures on different architectures
    https://github.com/scikit-image/scikit-image/issues/6994
    https://github.com/scikit-image/scikit-image/issues/6995
    -> should not hold up announcement
  - Status on conda-forge https://github.com/conda-forge/scikit-image-feedstock
  	- [How to trigger bot to build?](https://conda-forge.org/docs/maintainer/updating_pkgs.html#how-does-regro-cf-autotick-bot-create-automatic-version-updates)
  - [Tweet](https://twitter.com/stefanvdwalt/status/1666131344211197952)
- Version switching
  - [Broken on mobile, being fixed](https://github.com/pydata/pydata-sphinx-theme/pull/1342)
  - Switching to a different version of the docs, it sometimes does not find a nearby page (since page structure changed)
      - Dev *release notes* -> 0.20 via version switcher; won't find release notes (directory structure changed), but should navigate up one level to root of docs.
      - Same problem on pydata-sphinx-theme: 
        https://pydata-sphinx-theme.readthedocs.io/en/stable/examples/index.html
        Jump to v0.9
      - Lars will open an issue on pydata-sphinx-theme
- [Release notes script](https://github.com/scikit-image/scikit-image/pull/6961)
  - longterm put it in Scientific Python
  - Publish both rst and markdown versions of release notes
  - grab PR descriptions from code fence
    ````
    ```release-notes
    some text
    ```
    ````
  - Jarrod will update release notes with much simpler process we now follow after this is done
- [NumPy 1.25 API backward compatible C compilation](https://numpy.org/devdocs/dev/depending_on_numpy.html#build-time-dependency)
	- Once 1.25 is out, we can set >=1.25 as our build dependency
- [Script](https://github.com/stefanv/minutes) by Stéfan to push meeting notes automatically?
	```
	python minutes.py https://hackmd.io/-HCxhoU4RSiC-RzVMyoweg scikit-image/skimage-archive /meeting-notes/2023
	```
	Does not yet have an option to add a postfix such as "europe" or "pacific", as we currently do.
- Keep monitoring NumPy trig reimplementation, and impact on our test suite

- ImageIO is currently breaking our test suite; we're adding an upper pin until it can be resolved
	- Jarrod is making a PR to add `skimage.io` tests to ImageIO CI
