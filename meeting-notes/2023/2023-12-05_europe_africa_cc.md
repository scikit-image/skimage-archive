# scikit-image Community Call

- **Time:** Tuesday, November 21, 2023, 16:00 – 17:00 UTC
- **[Join video call via Jitsi](https://framatalk.org/skimage-community)**
<!-- - **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)** -->
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Lars, Stéfan

## Agenda 12/05

- mybinder links for older versions
	- remove links from docs?
	- for next version: [fix jupyterlite build](https://github.com/scikit-image/scikit-image/pull/6974) in docs deploy
	- [things to investigate](https://github.com/scikit-image/scikit-image/pull/6974#issuecomment-1841126696)
	- Looks like pyodide has a [working meson build](https://github.com/pyodide/pyodide/pull/3874)
	- scikit-learn's JupyterLite also not version-matched; see https://scikit-learn.org/dev/lite/lab/
		- Doesn't work on FF, but under Chrome that gives version 1.3.1 when dev is 1.4.dev0
	- We use CircleCI to generate docs previews, and [GH Actions](https://github.com/scikit-image/scikit-image/blob/main/.github/workflows/build_docs.yml) to upload devdocs
		- So, we want to **TODO** build docs / jupyterlite in parallel, upload the docs and wheel as artifacts, and then have a dependent job that merges the two and uploads
		- Each devdocs push currently makes a new commit; oops! **TODO** Change it so that we amend previous devdoc commits.
			- Is there a way to host devdocs and regular docs in different locations?
				- If we deploy with Netlify, we could use redirects, but GH Pages doesn't support that.
- skimage dev wheels with NumPy 2.0
  - https://github.com/scikit-image/scikit-image/pull/7251
  - under investigation in
    - https://github.com/serge-sans-paille/pythran/issues/2157
    - [Patch to Numpy](https://github.com/numpy/numpy/pull/25313) should be merged today
- Take note of [plan for skimage 2](https://discuss.scientific-python.org/t/yet-another-pathway-towards-skimage-v2/859/12)
- Lars is working on
  - Update deprecation tooling in [Add new deprecate_parameter helper #7256](https://github.com/scikit-image/scikit-image/pull/7256)
    - Reduce work for [deprecations in skimage2](https://github.com/scikit-image/scikit-image/wiki/API-changes-for-skimage2)
    - Should also fix [Detecting stacklevel for deprecation warnings is broken #7257](https://github.com/scikit-image/scikit-image/issues/7257)
  - [Add thin-plate splines warping #7040](https://github.com/scikit-image/scikit-image/pull/7040)
    - Think it's ready for general review
  - Re: keyword-only arguments, we can be fairly bullish about moving to keyword-only arguments, but will likely never force positional only arguments, i.e.:
	```python
	f(1, 2) — OK
	f(x=1, y=2) — OK
	f(1, 2, extra_arg=3)

	def f(x, y, *, extra_args=None):
			...

	# but never

	def f(x, y, /, *, extra_args=None)
	```
  - add typing stubs
    - emulate what matplotlib did, goal `stubtest` should pass at least on test suite
    - skip internal type validation for now, we care most about public API facing users
    - preparation for once typing for NumPy arrays can do shapes
- Low hanging fruits
  - [Rework docstring of ImageCollection #6988](https://github.com/scikit-image/scikit-image/pull/6988)
