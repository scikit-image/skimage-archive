# scikit-image Community Call

- **Time:** Tue, 2024-01-14, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Aditi Juneja, Lars Grüter, Stéfan van der Walt


## Agenda

- [Debug flaky test_reproducibility on Azure since Dec 18 #7659](https://github.com/scikit-image/scikit-image/pull/7659)

- Azure warning for PRs
  - ["You should provide GitHub token if you want to download a python release. Otherwise you may hit the GitHub anonymous download limit."](https://dev.azure.com/scikit-image/scikit-image/_build/results?buildId=12061&view=logs&j=5761e92d-7017-5e7c-b719-867af7afe737&t=38d043ab-036c-58b0-8e78-c77e54865583&l=9)
  - Lars: is this fine?
  - We'll deal with it if it becomes a problem.

- [WIP: Refactor to skimage.morphology.footprint_ellipse #7628](https://github.com/scikit-image/scikit-image/pull/7628)
  - Reproducing the old behavior vs using the same algorithm for ellipse, ball, etc...?
  - Splitting out decomposition into extra functions like `footprint_decomposed_ellipse` would make behavior easier to explain.
  - Or we don't enforce the `footprint_*(shape=(...))` everywhere and use `diameter=` or `radius=`.

- [Basic infrastructure for dispatching to a backend #7520](https://github.com/scikit-image/scikit-image/pull/7520#discussion_r1812140971)
  - [Spatch requirements for reuse in other libraries #1](https://github.com/scientific-python/spatch/issues/1)
  - (partial?) list of previous discussions: https://discuss.scientific-python.org/t/api-dispatching-in-scikit-image-summary-and-future-enhancements/1497
  - [principles discussion](https://github.com/scientific-python/spatch/issues/1)
  - Discuss how to allow backends to hook into the test suite
    - We don't know under which circumstances a backend will accept a function + args for dispatching
    - Therefore, we'd have to rely on the backend to decide which parts of the test suite it wants to run; or, at minimum, which functions it wants to run during testing
    - Does it make sense, even, to try and provide dispatch libraries with our test suite? They may support different accuracies, not care about warnings, type checks, etc. etc.
      - Find out how cucim team is currently testing against skimage API



### Feedback on dispatching design

- Currently in https://github.com/scikit-image/scikit-image/pull/7520 - dispatched to the alphabetically first backend
- Type-based dispatching 
    - Limitation: one array type can only be supported by one backend (ref. https://github.com/scikit-image/scikit-image/pull/7520#discussion_r1880480398)
- ‘Backend-name’-based dispatching - implemented in https://github.com/betatim/scikit-image/pull/1
    - Here also we do require the user to pass in the array type compatible with the backend(s) they want to use; scikit-image don’t do any internal array conversions(not purely ‘Backend-name’-based)
    - `SKIMAGE_BACKEND_PRIORITY` used to set backend priority, or just a single backend, and disable dispatching
    - dispatching on/off by default
    - Needs feedback on this! should I proceed with this?
    - or something like `ski.set_backend_priority("backend(s)")`
    - **conclusion from the discussions** - env variable approach is good enough for a prototype implementation.
- Hybrid approach?
- Performance-based dispatching
- ...


### ToDos(for dispatching):

- After https://github.com/scikit-image/scikit-image/pull/7520 and https://github.com/betatim/scikit-image/pull/1 (need to fix tests in this PR) are merged in, integrate a basic backend setup in cucim; get feedback from cucim people! Lars will try to review these this week.
- [Aditi] Testing backends using scikit-image’s tests - backend provided the array conversion functions? or some other approaches? - discussed above.
- Documenting backend implementation(s):
    - Add it in the algorithms’ `__doc__`. any disadvantages to this?
        - `I am a little hesitant about doing this because it feels like you have to reach a little too deep into the Python box of tricks. Meaning there will be some weird side effects of doing this.` (from https://github.com/scikit-image/scikit-image/issues/7550)
    - Adding it on the scikit-image’s website
    - If @betatim wants to work on this, I [Aditi] can review/give suggestion on it; or else I can work on this!
- weekly scikit-image dispatch meetings?
    - poll to decide timing - https://crab.fit/splendid-red-swim-crab-961496
