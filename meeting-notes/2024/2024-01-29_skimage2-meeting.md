# Meeting notes "Coordinating skimage2" 

- January 29, 2024 at 20:00 UTC
- [Video meeting room](https://meet.evolix.org/skimage-meeting)
- [Discussion thread](https://discuss.scientific-python.org/t/yet-another-pathway-towards-skimage-v2/859/6)

**Participants:** Lars, Egor, Marianne, Josh, Jarrod, Stéfan, Juan

## Agenda outline

- Short presentation of latest transition plan (by Lars)
- **Focus: Discuss coordination**
- Optional: Discuss transition plan in detail
- Optional: Discuss typing scikit-image

## Coordination

- *Realistically, how much resources do we have?*
  - Paid hours left according to EOSS5 budget (Jan 2024):
    - Lars: ~1200 h
    - Marianne: ~250 h

- *How will we communicate about the work?*
  - Weekly dev update from Lars on discuss.scientific-python.org community list

- *How should work be prioritized?*
  - There's a new label: [`🥾 Path to skimage2`](https://github.com/scikit-image/scikit-image/labels/%3Ahiking_boot%3A%20Path%20to%20skimage2)
  - Use GitHub project (new) or rather a milestone? 
  - Requesting reviews?
    - Maintainers replied they were fine being requested PR reviews (using GitHub's feature).

- *How do we speed up consensus-seeking and decision-making for the new API?*
  - Clarify objection period for lazy consensus in SKIP 1: [#7020](https://github.com/scikit-image/scikit-image/pull/7020)

- *How can paid maintainers help with bottlenecks?*
  - Coordinate consensus-seeking periods and call votes?

- Stéfan: Request to core developers, for the six months starting around May:
  - Please attend community calls whenever possible
  - Please follow along with 2.0 issues on GH (we have to make decisions rapidly and move on)
  - Please review as much 2.0 transition code as possible

## Timeline & process

### Starting now

- Make as many [non-breaking changes](https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2#proposed-api-changes-doable-ahead-of-skimage2) as possible
  - **Note: There are not many releases left to complete deprecation cycles!**
- Concretize breaking-changes
  - e.g., which functions use implicit rescaling?
- Settle pending decisions
- Make skimage2 folder to make it very easy to play around with

### 2024-5, Last release with old API

- Release `scikit-image==0.24.0`
  - possibly version 1.0?
- Feature & bug freeze until transition is complete

### ~6 months, Transition to new API

- Every PR / change goes into a migration document

### 2024-11, Release candidate with new API

- Release candidate: `scikit-image==0.25.0`
  - identical with previous `scikit-image==0.24.0`
  - but has a warning to migrate or pin
  - and maybe make sure there are wheels for most recent Python (3.13/3.14) so more folks see the warning / migration plan (this may mean backporting build improvements and so be careful to isolate that work in standalone PRs)
  - *Give migration guidance as warnings in old API?*
- Release candidate: `skimage2`
  - new API and namespace `skimage2`
  - Version starts at 2.0.0
  - if technically possible, get `skimage2` package to give a helpful warning if `skimage` is imported but not present
  - What about https://pypi.org/project/skimage/
  - maybe grab https://pypi.org/project/skimage2/ soon

### 2025-01, Release new API

- Release: `scikit-image==X+1`
  - *Support & backporting for 1.5 years from here on?*
- Release: `skimage2`
- Update third-party documentation resources: StackOverflow, etc.

## Advantages & challenges

**User perspective:**

- Can use `skimage` and `skimage2` at the same time 
- Easy to explain
- With upgrade, users are notified about transition via warning
- With upgrade, user code isn't broken

**Maintainer perspective:**

- Don't have to maintain two APIs
- Decisions & breaking changes during short time frame

---

## Typing scikit-image

- We care about public API first
- Type description in docstrings will be ground truth
  - Automatic stub generation from docstrings, e.g, [docs2stubs](https://github.com/gramster/docs2stubs)
- CI does type checking only on test suite
- Expect iterative process
