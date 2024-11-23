# scikit-image Community Call

- **Time:** Tue, 2024-11-20, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Lars, Marianne, Stéfan, Jarrod

## Agenda

- EOSS5 interim report due on Jan 1, 2025
  - Need to ask NumFOCUS for financial report
      Reporting period: end date of previous report to submission date of current report
  - Extension for Marianne's ICA already went through, Lars's is still pending
  - Should get a few items from the skimage2 list in (prioritize these items and request reviews)
  - Lars will focus on releasing docstub v0.3 (minimal viable prototype) in time
    - Then update [Generate typing stubs with docstub #7546](https://github.com/scikit-image/scikit-image/pull/7546) to include first infrastructure in skimage

- skimage 0.25 release progress
  - [milestone](https://github.com/scikit-image/scikit-image/milestones/0.25)
  - Stéfan suggested to Lars that we also see if we can close the loop on [7566](https://github.com/scikit-image/scikit-image/pull/7566), [7292](https://github.com/scikit-image/scikit-image/pull/7292), [6892](https://github.com/scikit-image/scikit-image/pull/6892)
    - 7566: just needs a test
    - 7292: ready to merge, need to check CI failure on Windows
    - 6892: lazy loading is interfering with `lookfor`, Lars is debugging it; not super urgent
    - Will try to get all this merged today
  - [7504](https://github.com/scikit-image/scikit-image/issues/7504) can be closed
  - Double-checked that watershed fixes ([7071](https://github.com/scikit-image/scikit-image/pull/7071)) made it in ✓
  - Also review [path to skimage2](https://github.com/scikit-image/scikit-image/issues?q=is%3Aopen+is%3Aissue+label%3A%22%3Ahiking_boot%3A+Path+to+skimage2%22)
  - Timeline: end-of-week rc2

- Dispatching
  - Aditi received the NF Small Developer Grant
  - First PR to get over the line: [7520](https://github.com/scikit-image/scikit-image/pull/7520)

- General
  - [Marco Gorelli: Narwhals](https://www.youtube.com/watch?v=kPtUPe5Egak)
    - As close as we're likely to get to DataFrame API
  - [spin 0.13rc0](https://pypi.org/project/spin/0.13rc0/)
    - [extend built-in commands](https://github.com/scientific-python/spin/pull/248)
    - [pre-import for IPython](https://github.com/scientific-python/spin/pull/251)
    - [diff for NumPy](https://github.com/numpy/numpy/pull/27794/files)
  - Lars will reply to Juan about typing (going for the Annotated route)
    - Close the loop on [the discourse topic](https://discuss.scientific-python.org/t/typing-scikit-image/877/32)
    - For now, we can't easily get what we want without a mypy plugin:
      - We want to check, if input is annotated as, say, Mask, it cannot be passed into a parameter that expects an Image
      - At the same time, a Mask *can* be specified as an Array, otherwise users will *always* need to annotate their types
      - We cannot simply make parameter requirement "Mask | ndarray", because then Image will also pass (being an narray)
      - Logic we need: "if annotated as Mask, Image, etc., this parameter only accepts *Mask*"
      - As we add the type annotations, this will force us to define precisely what we mean by *Mask*
