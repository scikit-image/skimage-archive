# scikit-image Community Call

- **Time:** Tue, 2024-10-22, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Aditi Juneja, Stéfan van der Walt, Marianne Corvellec, Lars Grüter, Lex, Jarrod Millman

## Agenda

- [NumFOCUS board election](https://github.com/numfocus/elections)
  - How do we allocate our 3 votes as a member project
    - Something like [Instant-runoff voting](https://en.wikipedia.org/wiki/Instant-runoff_voting) might be a good fit if we can implement it
  - Action: short team meeting to achieve consensus on vote 

- Release 0.25.0
  - Status?
  - Pyodide wheels: ping [Agriya Khetarpal](https://github.com/agriyakhetarpal)

- EOSS5 no-cost extension
  - > approved internally and [...] the funder, SVCF [...] should be in touch with the amendment within the coming weeks. 
  - new grant end date: January 31, 2026
    - At current burn rate will spend funds ~October/November 2025
  - interim report due: 1/1/2025
  - final report due: 4/1/2026

- Move gallery testing into its own shorter running workflow without running the test suite?
  - Do only a single gallery run, in parallel; disable for other docs builds
    - Should not need to build docs on >1 platform
  - Can also reduce coverage; not needed on multiple platforms
  - Mark certain tests as slow, and only run them on a single target (rolling ball, e.g.)
  - Ensure we have caching on repeated PRs

- **Review coordination & triage**
  - [Feature/enhance plot matched features #7541](https://github.com/scikit-image/scikit-image/pull/7541), waiting for 2nd approval
    - [x] Added cycle example to docstring -> [name=Lars] to rephrase
  - Anything else...?

- Dispatch meeting: [notes](https://hackmd.io/4oRcgg9EQeWQ18Mv2sdfMA) | [Aditi's topic summary](https://hackmd.io/7Eb4GiNMQXCwTbgW0DZ10A)
