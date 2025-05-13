# scikit-image Community Call

- **Time:** Tue, 2025-05-06, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Lars, Matthew


## Agenda (2025-05-06)

- [Deprecate estimate method in favor of class constructor #7771](https://github.com/scikit-image/scikit-image/pull/7771)
	- Discuss version target of deprecation (2.0 vs 2.x)

- [Refactor thresholding to segmentation #7781](https://github.com/scikit-image/scikit-image/pull/7781)
	- proposed API needs review
	- Lars is porting last tests to `ski.segmentation`
	- Worry about preserving git history? -> don't waste time on this

- Adoption roadmap for docstub
	- DONE implement grouping of error messages
	- NEXT implement ratchet (max allowed errors)
	- [Only set up stub generation with CI #7546](https://github.com/scikit-image/scikit-image/pull/7546)
	- Address docstub errors in groups, keep PR size reasonable and allow discussion of desired syntax.
	- Add type checking on stubs and test suite
	- Distribute stubs...

- Matthew's FundamentalMatrix PR

Other PRs that need review:

- ...
