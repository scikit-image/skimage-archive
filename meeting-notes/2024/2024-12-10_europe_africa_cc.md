# scikit-image Community Call

- **Time:** Tue, 2024-12-10, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Lars, Stéfan

## Agenda

- [0.25.0 release](https://github.com/scikit-image/scikit-image/milestone/29)
- [Refactor to skimage.morphology.footprint_octagon #7626](https://github.com/scikit-image/scikit-image/pull/7626)
  - How should we adapt `m, n` to API using `shape`?
  - Lars: figured out for `decomposition=None`
  - similar problem but less severe for `star`
- [Lazy load legacy imports in skimage top module #6892](https://github.com/scikit-image/scikit-image/pull/6892)
  - Settle [discussion](https://github.com/scikit-image/scikit-image/pull/6892#discussion_r1871799519): include builtins like `__file__` in `__dir__()`?
  - Python docs allow for both solutions
- Marianne & Lars: currently working on EOSS5 interim report
  - NF will provide financial report by 22 November
- Intermittend CI failures are due to plot.ly / kaleido
  - [Experimental PR: update to rc versions](https://github.com/scikit-image/scikit-image/pull/7623)
    - Reported [bug in plotly serialization](https://github.com/plotly/plotly.py/pull/4926)
    - Waiting for rc1 at [plotly releases](https://github.com/plotly/plotly.py/releases)
  - Plotly performance is not great: slows down build, and is resource heavy in browser; should we consider replacing?
    - Should get Marianne's input on this first
