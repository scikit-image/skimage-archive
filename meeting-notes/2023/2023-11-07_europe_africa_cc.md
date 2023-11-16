# scikit-image Community Call

- **Time:** Tuesday, November 7, 2023, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Cris Luengo, Lars Grüter, Adeyemi Biola, Peter

**Moderator:** Stéfan

## Agenda

- [**Fix morphology PR #6695**](https://github.com/scikit-image/scikit-image/pull/6695)
	- Correctness of opening / closing with mirroring of structuring element
	- Boundary conditions were not ideal
		- Ideally, we'd change the default for 2.0, but for now we have the non-ideal choice for backward compatibility
		- The binary / grayscale versions should do the same thing; that is not currently the case
		- Not only binaries, but padding is switched: left to right
  - PR was verified to be correct, then generated new results (only changed for even-sized elements); that data was committed on [GitLab data repo](https://gitlab.com/scikit-image/data/-/merge_requests/23)
- **Typing**, some thoughts
  - input parameter `p: float | Sequence[float]`, then internally `p = np.array(p, ndmin=1)` -> mypy will complain
    ```
    Incompatible types in assignment (expression has type "ndarray[Any, dtype[floating[Any]]]", variable has type "float | ndarray[Any, dtype[float]]")
    ```
    - Not really sure what would be a good solution here
  - [`ArrayLike`](https://numpy.org/devdocs/reference/typing.html#numpy.typing.ArrayLike) 
    - can't be used with `NewType`
    - Cannot dictate scalar type
- [**Thin plate splines PR #7040**](https://github.com/scikit-image/scikit-image/pull/7040)
	- Lars will review after morphology PR goes in
	- Biola responded to all of Marianne's comments
	- `spin` issue: hopefully resolved by upgrade
	- Working on gallery application example
- Next release around beginning of 2024
