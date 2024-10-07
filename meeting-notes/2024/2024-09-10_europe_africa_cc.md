# scikit-image Community Call

- **Time:** Tue, 2024-09-10, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**


**Present:** Aditi Juneja, Erik Welch, Lars Grüter, Stéfan van der Walt, Adeyemi Biola

## Agenda

- Backend progress
  - Multiple PRs related to backend
  	- [Basic infrastructure for dispatching to a backend #7520](https://github.com/scikit-image/scikit-image/pull/7520)
  	- [Adding dispatching to scikit-image #7513](https://github.com/scikit-image/scikit-image/pull/7513)
  	- [WIP: cucim backend for skimage #7466](https://github.com/scikit-image/scikit-image/pull/7466)
  - Erik's plan this week is to come up with a way to test the backend system
  - Get a minimal example going using `spatch`
  - Erik, Aditi, and Tim will coordinate and resolve open PRs

- EuroSciPy sprint report
  - Reviewed skimage2 API changes list
  - We now have a long TODO list of items we can execute before the skimage2 transition
  - And then, focus on making the transition itself (which requires a fair amount of sensitive changes to, e.g., transformations)
  - [brief weekly report on skimage2 sprint](https://discuss.scientific-python.org/t/weekly-reports-on-scikit-image-development-2024/1328/6)

- docstub
  - done: minimal prototype
  - next: figuring out how to test with mypy
  - longterm: draft PRs for scikit-image & networkx

### Review opportunities

- [Fix several watershed issues (off-center markers, watershed_line) #7071](https://github.com/scikit-image/scikit-image/pull/7071) needs 2nd approval
	- Finding a 2nd review might be difficult, maybe merge regardless?
