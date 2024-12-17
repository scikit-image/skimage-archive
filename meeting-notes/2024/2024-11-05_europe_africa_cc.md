# scikit-image Community Call

- **Time:** Tue, 2024-11-05, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**


**Present:** Stéfan van der Walt, Lars Grüter, Aditi Juneja

## Agenda

- Remove docstring manipulation in `RegionProperties` during runtime (see `_install_properties_docs`)?
  - It's brittle, see [#7448](https://github.com/scikit-image/scikit-image/pull/7448)
  - Doesn't work with our planned use of docstub
  - Property descriptions in `regionprops` tend to be short and lacking literature references
  - Suggested fix: expose `RegionProperties` and each `@property` in HTML docs, and document the properties there

- [0.25.0 release?](https://github.com/scikit-image/scikit-image/milestone/29)
  - [Use scipy.sparse arrays #7576](https://github.com/scikit-image/scikit-image/pull/7576)
    - Make a TODO item on the pytest warning handling
    - Should we [check before downcasting](https://github.com/scikit-image/scikit-image/pull/7576/files#r1824544991)?
  - Anything else holding it up?

- [feat: add mask parameter to graycomatrix function for selective computation #7544](https://github.com/scikit-image/scikit-image/pull/7544)
  - New feature would introduce slow-down or duplication, do we have a general stance on this?

- Speed-up CI
  - [Build docs in parallel instead of sequentially on Azure #7593](https://github.com/scikit-image/scikit-image/pull/7593), ready to review
  - Principle: test suite has to run, anything we add for "convenience" is OK but should not slow test suite down

- Progress on [pre-skimage2 list](https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2)
  - We have a NCE on the CZI grant until end January 2026
  - [Replace square, rectangle, cube with footprint_rectangular #7566](https://github.com/scikit-image/scikit-image/pull/7566)
    - Part of incremental changing selems to `footprint_*`
  - https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2

- Update the wiki

- NIH grant: postponing submission until next year, 4 June 2025
  - [Mechanism](https://grants.nih.gov/grants/guide/rfa-files/RFA-OD-24-010.html) 
  - Think about setting up survey


### Dispatching Topics

- Aditi: Narrative dispatching documentation - 3 parts
    - scikit-image users
        - How to use it (in general - `SKIMAGE_NO_DISPATCHING`, etc.)
        - Introspection/logging/warnings : DispatchNotification, etc.
    - Backend developers (on the [development page](https://scikit-image.org/docs/dev/development/index.html))
        - What makes up a valid backend?
        - entry_points : “skimage_backends”, ”skimage_backend_infos” (“implementation” and “info”)
        - How do things like `can_has` work?
        - How does scikit-image offer testing facilities for backends?
    - Implementation details
        - entry_point mechanism
        - Working and usage of the `dispatchable` decorator - how are function signatures handled?
        - Testing details
        - How does the backends’ metadata gets handled, etc.
    - Should some of it go into a SKIP-5? - https://scikit-image.org/docs/dev/skips/index.html
    - TODO [Aditi]: continue this (or other developments) in [PR#7513](https://github.com/scikit-image/scikit-image/pull/7513)

- Created [#dispatching](https://discord.com/channels/786703927705862175/1303422714987679754) channel on SP discord for day-to-day discussions

- Aditi: Some inconsistencies between scikit-image’s and networkx’s dispatching mechanisms
  - Which ones are necessary and why do they exist?
  - Eventually we should ensure ecosystem-wide consistency
    - `get_implementation` vs having the algorithms as the attributes of the entry_point object
    - Having some consistency in setup/private functions’ names : like steps (or functions involved) in fetching the backends (`all_backends()` vs `_get_backends()`) and then fetching the implementations from the backends, and loading the backend metadata (or info), etc. (adding these functions/setup in `spatch`?)
    - Meaning and usage of the term “backend info” in scikit-image vs networkx
    - Naming:
        - `can_has` vs `can_run`
        - `dispatchable` vs `_dispatchable`
        - `_backends.py` vs `backends.py` (maybe ok to have this difference, because both projects are organised differently)
    - Should NetworkX’s logging and BackendInfo be more modular like scikit-image’s?
  - [Lars] It would be best to address these once we have a good enough prototype in place. 
 
- [TODO] Letting users set the order of backends instead of hard-coding it.

- potential backend libraries, for reference, other than `cuCIM`?

- NumFOCUS’s SDG R3: might get notified tomorrow
    - If positive, next step would be - ICA form (draft): https://hackmd.io/@Schefflera-Arboricola/SynEV9vZ1x (contract will finalise within 1-3 weeks (based on the responsiveness of PI and contractor) of submitting the above form)
