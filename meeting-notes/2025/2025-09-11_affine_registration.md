# Affine registration

:::info
- **🕙 Time:** Thu, 2025-09-11, 7:30 – 8:15 UTC
- **[☎️ Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- **[📝 Meeting notes (this document)](https://hackmd.io/@mkcor/affine-registration)**
- **[📅 scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[📜 Archive – Meeting Notes](https://github.com/scikit-image/skimage-archive/tree/main/meeting-notes)**
- **[🤗 Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**
:::

## Agenda

**Present:** Jérôme, Juan, Loïc, and Marianne.

### Context

This online meeting aims at preparing the in-person mini-sprint to take place on October 1st (afternoon) and October 2nd (morning).
- Quick introductions.
- Logistics in Paris.

### Class-based vs. functional API

- In [PR #7421](https://github.com/scikit-image/scikit-image/pull/7421), the transform is 'just' a function which takes a reference  image and a moving image as inputs and returns the transformation matrix.
- vs. 0. initialization of the transform
    ```py
    import skimage as ski
    
    tform = ski.transform.Transform()
    ```
1. estimation of the transformation matrix
    ```py
    tform.estimate(reference_image, target_image)
    ```
2. display of the transformation matrix
    ```py
    tform.params
    ```

- We are going for a functional API.

### Final review for [PR #7421](https://github.com/scikit-image/scikit-image/pull/7421)

- We want this feature in the library!
- It implements the pyramidal affine tracking algorithm for image registration, as presented in chapter 7 of *Elegant SciPy*.
- It's already gone through several rounds of reviews.
- It contains the expected tests and docstrings.
- It comes with a gallery example.
- There is currently a discrepancy wrt SciPy's `ndimage.affine_transform` function because of the xy/rc coordinate convention.


### Resubmit PR
- [name=Jérôme]'s PR needs updating to resolve the merging conflicts which notably follow from our recent layout overhaul.
- [name=Marianne] I can take care of the above if that's helpful, it's tedious but it will make me super familiar with the feature.
- Decision from meeting: squash, merge, fix conflicts, resubmit as a new PR.

### Credit
In the process, keep authorship/credit for Jérôme of course, but also Sean and Juan!

### Implementation of ECC algorithm

- WIP [PR #7666](https://github.com/scikit-image/scikit-image/pull/7666) by [name=Loïc].
- It reimplements an algorithm from the OpenCV library.
- It's another possible solver for the affine transform.
- [name=Jérôme] explains it's a more careful approach, while the current one is more 'meta.'
- When we ship a first version for the affine registration, we can try and plug this ECC solver.
- Write up a gallery example using published images from [name=Loïc]'s physics lab.

### Terminology

Standardize terminology across transforms? In function signatures, the pair of input images are `image0, image1` when the order does not matter (symmetry).

Here we have:
- a *source* image (OpenCV: "template") -> reference_image
- a *target/destination* image (OpenCV: "warped image") -> moving_image

We may look up the current naming conventions in the literature and discuss this at the mini-sprint.
