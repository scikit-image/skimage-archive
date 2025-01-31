# scikit-image Community Call

- **Time:** Tue, 2025-01-28, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Agryia, Matthew, Lars, Stéfan, Aditi, Jarrod

## Agenda

- Thoughts on switching to [`src` layout](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/) (long-term)?
  - Our existing layout has caused and is causing friction, especially around pytest ([recent example (#7670)](https://github.com/scikit-image/scikit-image/pull/7670#issuecomment-2614123247))
  - No strong opinions expressed; probably fine to switch if it is not too disruptive for existing PRs

- [name=Agriya] [Factoring out data bundle](https://github.com/scikit-image/scikit-image/issues/7470#issuecomment-2617220300)
  - Split data into repositories: legacy / classic, test, extra / gallery. Tests depend on legacy and test data.
  - Do we make it pip installable? Unsure; we have `download_all`, `download_*` for the various categories.
  - Can consider publishing data bundles as part of the release to GitHub. But unclear how distributions will use those, unless they modify the cache path?
  - Potentially skip tests that rely on datasets being present, e.g, https://github.com/pybamm-team/pybamm-data/releases/tag/v1.0.1
  - Impact on downstream packagers related to licensing was discussed
  - Agriya: I will start out with adding install tags (both Meson native ones and custom ones), and see from there.

- [Basic infrastructure for dispatching to a backend #7520](https://github.com/scikit-image/scikit-image/pull/7520)
  - merging `get_implementation` and `can_has`
    - S: `can_has` was a joky name during the sprint; thought it would be replaced by something more meaningful
    - S: Need to document, for backends, that the `can_has` part needs to be very fast, since we need to cycle through various backends; maybe place some restrictions there on, e.g., whether imports are allowed during that process etc.
    - S: Think merging is OK, if it's simply "return quickly if you don't have it, otherwise do the work to return the function to be called"
  - what's left to do to merge this?
  - From the [poll](https://crab.fit/scikitimage-weekly-dispatching-meetings-382531), it seems **Wednesday(29th Jan, 2025) : 08:00 AM to 09:00 AM UTC** works for everyone
      - Meeting link - https://meet.google.com/iwo-bzjy-trq
      - HackMD notes - https://hackmd.io/@betatim/SJlpIwQgyl/edit

- CI updates
  - [Refactor gh scripts #7672](https://github.com/scikit-image/scikit-image/pull/7672/files)
    - `pyproject.toml` dependencies should be cleaned up
      - Try and make the subsets of dependencies orthogonal, and then rather have, e.g., tests depend on multiple categories
      - Can, in `pyproject.toml` , one extra depend on another extra? AK: Yes, pip 21 and later.
        - Requirements files also support this, with `-r` flag and relative paths.
    - Action: split into scripts for installing various types of dependencies, and add those steps where necessary: build, test, docs.

- ARPACK fix
  - S TODO: re-enable disabled test
  - [name=Lars] will merge
  - Priority for 0.25.2 release

- [Watershed regressions](https://github.com/scikit-image/scikit-image/issues/7661) due to merged improvements
  - Priority for 0.25.2 release
  - [name=Lars] will take a look as well

- SciPy 2025 submission deadline: 2025-02-26
  - Probably not attending: Jarrod, Lars, Stéfan

- Is EuroSciPy happening? Yes, [Aug 18 to 22, Krakow](https://euroscipy.org/2025/).
  - Plan sprint in wake of that conference since Stéfan, Jarrod and Lars are interested in going, should ask Egor, Juan, ...
  - S will post to the forum
