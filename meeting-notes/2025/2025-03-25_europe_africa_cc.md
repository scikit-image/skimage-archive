# scikit-image Community Call

- **Time:** Tue, 2025-03-25, 18:00 – 19:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- **Notes:** https://hackmd.io/-HCxhoU4RSiC-RzVMyoweg
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Matthew Brett, Marianne Corvellec, Aditi Juneja


## Agenda

### Transform API

Matthew started refactoring the API of our geometric transforms. Given a set of source
coordinates and another set (same number of points) of destination coordinates, the goal
is to estimate the matrix which transforms the former into the latter, as captured by a
few parameters (for scale, rotation, translation). The computation is thus an optimization
one, starting with some initialization.

Matthew explained how unsatisfactory the current initialization was, since the `estimate`
method does not use starting parameters. Also, the current `estimate` method returns `True`
or `False` (whether the optimization computation has converged or not), whereas we would
want *something* to return an actual transform (perhaps with parameter values None/NaN in
case of failure).

Open PR: [#7754](https://github.com/scikit-image/scikit-image/pull/7754)

### scikit-image in-person sprint

Marianne joined late and mentioned the in-person sprint which is scheduled to take place
over 2 (3?) days somewhere between Aug 12--16 in Vienna, Austria. But we haven't found a
venue yet.
Meanwhile, she will be participating in the
[GloBIAS workshop](https://globias-bioimageanalysts.github.io/2025-04-07-GloBIASDataCarpentry-Workshop/)
dedicated to updating the Data Carpentry image processing curriculum
for bioimage analysis practitioners, also in Vienna (or just nearby).

### Fundamental matrix

Matthew started looking at our implementation of the fundamental matrix, which transforms
the coordinates of image points as 'seen' by a camera into their coordinates as seen by a
different camera. Another pair of eyes would be welcome; Marianne said she would have a look.

Open issue: https://github.com/colmap/colmap/issues/3222
Reference paper: https://users.cecs.anu.edu.au/~hartley/Papers/fundamental/fundamental.pdf

### Dispatching

* Aditi is working on a draft PR: [#7727](https://github.com/scikit-image/scikit-image/pull/7727)
* She would like some feedback on the newly added environment variable(s) and context manager approaches to dispatch to different backends -- see [PR#7727](https://github.com/scikit-image/scikit-image/pull/7727)
    -- maybe from someone who works with large image data and uses / has used scikit-image
	  (i.e., an actual user of dispaching)?
* The question is about handling/passing environment variables
  - See how other projects (e.g., Matplotlib, Dask, NetworkX) do it?
  - Matplotlib backends: https://matplotlib.org/stable/users/explain/figure/writing_a_backend_pyplot_interface.html#entry-point (uses entry-points)
    Matthew admits that the consequences of changing backends in Matplotlib
    (i.e., figures rendering differently) are not the same as changing backends
    in an image processing pipeline (i.e., possibly getting different results). 
    Matplotlib's dispatching?
    - Aditi mentions Dask's [entry-point based dispatching](https://docs.dask.org/en/latest/how-to/selecting-the-collection-backend.html):
    context manager (`with dask.config.set({"array.backend": "cupy"})`), knowing
    that Dask already had global configs set via the same context manager
    (https://docs.dask.org/en/latest/configuration.html).
