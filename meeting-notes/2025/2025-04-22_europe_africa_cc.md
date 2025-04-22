# scikit-image Community Call

- **Time:** Tue, 2025-04-22, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Matthew, Lars

## Agenda (2025-04-22)

- [Refactor fundamental matrix scaling #7767](https://github.com/scikit-image/scikit-image/pull/7767)

- Link to this file changed? Owner: Scientific Python -> Stéfan
  - https://hackmd.io/@scientific-python/HJWUBDVNi/edit
  - Update calendar link

- status [skimage2](https://github.com/orgs/scikit-image/projects/4)
- status [skimage sprint @ EuroSciPy](https://discuss.scientific-python.org/t/1691)
- status docstub and typing scikit-image
	- Prototype is only missing minimal documentation
	- Demo/draft: [Generate typing stubs with docstub #7546](https://github.com/scikit-image/scikit-image/pull/7546)
	- Present somewhere? Conference? Offer EuroSciPy backup talk?
	- Integrate https://docs.basedpyright.com/latest/
- CI improvement PRs
  - [#7752: make PR when main fails](https://github.com/scikit-image/scikit-image/pull/7752)
  - [#7749: only test dependencies of modified modules](https://github.com/scikit-image/scikit-image/pull/7749)
  - [#7756: try and utilize ccache to improve build time](https://github.com/scikit-image/scikit-image/pull/7756)
    - S: Draft still; still struggling to get the optimization level right, which I suspect is preventing caching
    - Also experimented with doing one build per platform, and then testing different configurations: [example CI graph](https://github.com/scikit-image/scikit-image/actions/runs/13961049071?pr=7756)
  - S will discuss this with Jarrod as release manager

- [Logo redesign](https://discuss.scientific-python.org/t/scikit-image-logo-redesign/536/26)
	- Maybe iterate a bit more and settle on a few candidates
	- Stéfan suggests to pitch those to a designer for polishing
