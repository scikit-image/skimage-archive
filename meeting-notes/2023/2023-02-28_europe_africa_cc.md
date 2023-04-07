# scikit-image Community Call

- **Time:** Tuesday, Feb 28, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Lars

**Moderator:** -

## Agenda

- Release 0.20
  - Final PR updating the release notes: [Release notes 0.20.0 #6766](https://github.com/scikit-image/scikit-image/pull/6766)
  - How to spend less time on future release notes
  	- Main requirement is documenting API changes
  	- We could add a snippets to PR description / merge commit, and parse it out with tool like
  	  https://github.com/executablebooks/github-activity
      - Annoying if forgotten in merge commit. May want to have backup mechanism for PRs where snippet is forgotten. Label?
      - How about: label API change PRs, and ensure that those PRs contain a snippet like:
      
            ```release-note API
            Some text here
            ```

	      Changelog tool can then capture the above.
- [Prepare CI configuration for merge queue #6771](https://github.com/scikit-image/scikit-image/pull/6771)
    - Stéfan: Azure pipeline config already points at `azure-pipelines.yml`
    - Lars: to update Azure pipelines config, then we can try it as soon as release is out 
- Outreachy internship preparation
  - Marianne & Lars submitted two project proposals for scikit-image: https://www.outreachy.org/communities/cfp/scikit-image/
  - Still need to prepare for application period starting March 6th: 
    - Go through "Good first issues"
    - more lists like [Add docstrings to every submodule in skimage #6761](https://github.com/scikit-image/scikit-image/issues/6761)
  - Outreachy is concerned with non-OSI-approved [GraphicsGems-EULA covering `_adapthist.py`](https://github.com/scikit-image/scikit-image/blob/7f0c8fe7c1e47d233f6043bfd569f04efe1b593d/LICENSE.txt#L55-L56); [EULA text](https://github.com/scikit-image/scikit-image/blob/7f0c8fe7c1e47d233f6043bfd569f04efe1b593d/LICENSE.txt#L142)
  	- We have a response prepared; Stéfan reached out to Erich, Graphics Gems maintainer to see if they're willing to adopt a standard license.
  - Does scikit-image have any ties with companies or organisations other than NumFOCUS?
    - Stéfan: no
- [Showcase pydata-sphinx-theme #6714](https://github.com/scikit-image/scikit-image/pull/6714)
  - Mostly done, version switcher sometimes leads to 404 when a path doesn't exist in other versions (shouldn't happen according to Pydata docs). Maybe it's an issue with the CircleCI server?
  - Stéfan suggests https://witchhazel.thea.codes for syntax highlighting, Lars to look into it or another alternative
  - Stéfan: maybe number content of User guides? There's a [toctree option `:numbered:`](https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#directive-toctree) to do so
  - Stéfan to look into porting main website to Hugo
- scikit-image (Juan, Lars) might be at the SciPy 2023 tutorials together with Napari 🎉
