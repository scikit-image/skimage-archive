# scikit-image Community Call

- **Time:** Tue, 2025-02-11, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Lars, ?

## Agenda

- 0.25.2 release
  - Last issue [New watershed (in 0.25) does not give same results #7661
](https://github.com/scikit-image/scikit-image/issues/7661)
    - Fix in [Don't assign -inf to watershed markers #7702](https://github.com/scikit-image/scikit-image/pull/7702) 
      - Juan approved, ready to merge?


- [Basic infrastructure for dispatching to a backend #7520](https://github.com/scikit-image/scikit-image/pull/7520)
  - Lars approved
  - Waiting for at least 1 additional approval and the 0.25.2 release
  - Follow-up discussion around approach based on environment variable now in [Enabling backend priority #1](https://github.com/betatim/scikit-image/pull/1)
  - https://github.com/rapidsai/cucim/issues/829
  - Marianne made some small suggestions, would be easier for Aditi if we made those in another PR to avoid merge conflicts on Aditi's side. Lars will ping her about it.
  - Lars to check-in with Jarrod about when to release 0.25.2 and if feature branch is a possiblity
