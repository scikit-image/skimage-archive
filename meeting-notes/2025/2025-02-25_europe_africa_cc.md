# scikit-image Community Call

- **Time:** Tue, 2025-02-25, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Aditi, Matthew, Stéfan

## Agenda

- [Aditi] explaining dispatching in scikit-image to Matthew
    - https://github.com/scikit-image/scikit-image/pull/7520
    - https://github.com/Schefflera-Arboricola/skimage-j4f
- Discussed approaches for automatic testing for backends:
    - Which tests to run?
        - testing only fully supported functions by a backend; cannot test partially supported ones(i.e. that returns `False` at `can_has`)
        - Also what about the tests that are not testing a backend supported function but is running a backend supported funtion inside it? should we run that or not? in networkx we do run such functions and `xfails` the rest.(set by an env variable)
    - can we do automatic testing without the conversion of arrays?
        - can we make scikit-image's testing code to work with all types of arrays?
        - testing utility is optional for backends
            - backends supporting numpy arrays can easily test their backend using scikit-image tests just by setting the `SKIMAGE_BACKENDS` env variable
            - backends supporting other than numpy arrays:
                - can either write their own tests
                - or can convert their array into numpy array and then run the scikit-image tests.
                    - conversion could happen either hard coding the testing input arrays into the apt type or having convert functions
            - backend only convert if/when they want to test their backend..

    - [ToDo: Aditi] Create an issue on it for further dicussions
- How do we see array API adoption and dispatching in scikit-image’s future?
    - [Stéfan] scikit-image cannot adopt the array api standards because of Cython extensions
