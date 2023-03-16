# scikit-image Community Call

- **Time:** Tuesday, Mar 14, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Jarrod, Lars, Biola

**Moderator:** Stéfan


## Agenda

- [Prepare CI configuration for merge queue #6771](https://github.com/scikit-image/scikit-image/pull/6771)
    - Ready to merge... → merged
    - Lars will post on forum to let team know
- [Showcase pydata-sphinx-theme #6714](https://github.com/scikit-image/scikit-image/pull/6714)
  - Stèfan will look into porting main website to Hugo
  - Discussed structure of documentation; project -> about & developer guide
  - Add user guide to panels; removing trailing `...`
  - Automatically list release notes, so we don't have to update after each release
- EOSS3 report
- Archive
  - Name it `skimage-archive` to avoid conflict with other `archive` repos
	- Grant proposals
	- Grant reports
	- Outreachy proposals
- Discussion around skimage2 transistion
  - https://github.com/scikit-image/scikit-image/milestone/23
  - SKIP5: pathway to skimage2 + concrete summary of API changes absolutely needed
  	- Want to keep those changes to a minimum, and make them explicit
	- The milestone needs a review (unify milestone, label, project)
		- In NX they had a conference call and sorted it out pretty quickly
		- We should probably be a bit aggressive in closing issues
- Outreachy
  - We're in the application period, where we work together to get to know one another
  - Introduced to Biola
  - Lars asked feedback on issue difficulty and onboarding
- Necessity of point releases / backports
	- Volunteer, under-resourced, need to choose our battles
	- Backporting + bug-fix releases causes cause churn and extra work
	- Release instructions needs rewrite: half-assume release branch, half-assumes main branch
		- main branch release is more straightforward
		- Can document a "maintenance branch as needed" workflow as a separate document / section
		- Point releases are not often needed, unless a mistake was made in the published version
			- Thus, rc's have much reduced the need for point releases
	- Rather focus on more frequent releases, keeping main branch in good shape (last release it took a lot of work to get things running again)
    - With more frequent releases, need to change deprecations to be time based (how will users handle that?
    	- Simplest messaging may be "won't be deprecated before 0.23" / "will be deprecated with 0.23 or later", and then we just ensure that we don't deprecate before ~1yr has passed
  - Especially important to get releases smooth in anticipation of skimage2 transition starting soon
