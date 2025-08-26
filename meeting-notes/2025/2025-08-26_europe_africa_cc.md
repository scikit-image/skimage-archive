# scikit-image Community Call

:::info
- **🕙 Time:** Tue, 2025-08-26, 17:00 – 18:00 UTC
- **[☎️ Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)** <!-- - **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)** -->
- **[📝 Meeting notes (this document)](https://hackmd.io/@scientific-python/HJWUBDVNi)**
- **[📅 scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[📜 Archive – Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[🤗 Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**
:::


## Agenda (2025-08-26)

**Present:** Lars, Stéfan, Matthew

- [Update SKIP 4 #7866](https://github.com/scikit-image/scikit-image/pull/7866)
  - Ready for review

- [Simplify build wheel configuration by using of pyproject.toml configuration #7877](https://github.com/scikit-image/scikit-image/pull/7877)
  - Still not passing, open questions from Grzegorz
  - [name=Lars Grüter] will have a look again
  - Ideally we want to make use of our pool of available runners, don't want to wait 2+ hours for jobs to complete / fail

- Elena's [Gaussian pyramids question](https://forum.image.sc/t/unclarity-about-laplacian-pyramid-transform/115976/1)

### 2to1 adapter suggestion

In v1:

```python
@parse_preserve_range
def func(...):  # v2 compatible impl
    ...

def parse_preserve_range():
    ... call img_as_float on input ...
```

In v2:

```python
from skimage.foo import func as func_v1

func = rm_adapters(func_v1)
```

Benefits: can immediately polish up v2 implementation, backword compat code goes into discardable adapter.

It is not guaranteed that this approach will work for all cases, but may cover a fairly large number of them.
May require some docstring footwork: replacing / adding parameter descriptions.
