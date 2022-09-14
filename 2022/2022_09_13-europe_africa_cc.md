# scikit-image Community Call

**- Time:** Tuesday, September 13, 17:00 UTC
**- Place:** [Zoom Meeting](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)
**- Notes:** https://hackmd.io/@alexdesiqueira/skimage_cc

- [scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)
- [Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)

**Present:** Lars, Marianne, Alex, Greg, Stéfan

## Maintenance

- Update on dormant PR management?
    - Lars has submitted PR [#6506](https://github.com/scikit-image/scikit-image/pull/6506)
    - Time limit: NumPy uses something along these lines (6 months)
    - Would the label apply to older issues? Or only the new ones?
        - (Lars) As far as I understand, would work for all of them
        - Limit: 30 items/run
    - Is it a bot?
        - GHA: https://github.com/scikit-image/scikit-image/pull/6506/files
        - 180 days after stale-ing, it posts a message
    - What about the Kanban board?
        - GH doesn't do this automatically (labeling)
        - Maybe it wouldn't take too much time, though
        - (Stéfan) Without active maintenance, boards quickly go out of sync
        - (Lars) Don't have the permissions to make it public; willing to work on it [Fixed permissions for contributors to make boards public]
        - Maybe some steps can be automated?
            - Might be possible via an Action
            - (Stéfan) How does a bot know that a label was removed, and should not be reapplied?
                - Removing the label would count as activity, therefore will not be added back
- (Alex) Shouldn't we always have one PR corresponding to one issue?
    - Example: (#6491, #6492) pair
        - The proposed function are one-liners, since they are wrapping ndimage functions.
        - Should we start with a gallery example?
    - Where should the discussion take place? Publicly, on Discourse?
    - How popular should an algorithm be to be implemented? cf. recent PR #6488
- 0.20 release?
    - Would it be for python 3.9, 3.10, 3.11? 
        - 3.8 will also be included, it's still within 48 month support window, being released October 2019
    - Are we following the same schedule as NumPy (NEP29)?
    - Greg will teach us (Alex, Lars, Marianne) about the release process
    - Even if the release is not ready, we need to test whether the library works with python 3.11
- skimage-tutorials, merging lectures and solutions would decrease maintenance burden (1 file instead of two)
- Align skimage2 (SKIP4) with proposed typed API in EOSS5 proposal?
	- Juan: "the typed, protocols-based API *is* the skimage2 API"
	- Marianne +1's the above
- Missing 0.19.3 docs
    - Compressed docs repo (gh-pages branch) into one commit: it's now 65MB instead of 10GB!
    - Missed step in release process?

## Community management

- Code of conduct: whether and if, how, to involve PSF CoC committee [long discussion, not all captured here]
  - Talk at EuroSciPy on contributor experience
      - Said CoCs are only really effective with independent committee. Currently 3/4 are core devs. 
      - Said quick shoutout and link to CoC during meetings is very valuable to some
  - PSF offers their trained CoC work group to each Python project, would require using their CoC?
      - Maybe as a backup option?
      - Maybe sorting things our in your community could be more useful
  
## Education and Dissemination

- Lars did mini-sprint at EuroSciPy
    - Our list of good first issues is not up to date
    - In the future, would be good to prepare this in advance of sprint
    - Enjoyed the maintainer track
- Greg signed up to showcase skimage at CZI meeting
- Greg, Stéfan attending NumFOCUS annual meeting next week
