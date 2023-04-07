# scikit-image developer hackathon, BIDS, 2020-02-{27,28}

<!--
Join via [Zoom](https://monash.zoom.us/j/284282585)
-->

Present: Stéfan, Emma, Alex, Juan

## Items from the previous meeting

- Stéfan to review 3544
- Mark to show an example PR of how a deprecator can be left in place even after the version has changed. DONE: https://github.com/scikit-image/scikit-image/pull/4464
- JNI Example PR that shows how the `_` modules can be used to avoid ultra long and confusing tracebacks.

## Agenda

### scikit-image 1.0 goals/non-goals

Initial discussion aiming to become a SKIP. See [notes from 2020-02-17 Pacific meeting](https://github.com/scikit-image/meeting-notes/blob/master/2020/2020-02-17.markdown)

Proposals:

- deprecate all range conversions/assumptions, opting for user information about built-in rescaling functions
    - Motivation: large proportion of user confusion is "why is my image black" or "why have all my values changed"
    - Alternative: deprecate *most* range conversions, except for functions where a known range is absolutely necessary.
    - See [#3009](https://github.com/scikit-image/scikit-image/issues/3009)
    - Can we also get input from Tom Caswell and Hannah Aizenmann about relaxing range assumptions in mpl? (RGB float images must be in [0, 1])

    *Notes:*

    - We'd like to get rid of implicit data range assumptions based on data-type
    - Proposal: remove assumptions, where possible, and write pipelines as follows:
        `rescale(image, (0, 1)) -> func1 -> func2 -> rescale( ... if desired ...)`
    - Initial type annotations
        - Image (ndarray of int/float)
        - Label array (ndarray of bool)
        - Graphs (RAG)
        - Regionprops
    - Issues to consider:
        - Functions like `exposure.equalize_adapthist` (? maybe not best example), that operate only on integers
        - Functions that takes in floats (any range) and returns ints (output range defined)
        - Functions that require knowledge on the range of input <-- This problem is solved by normalizing range at beginning of pipeline
        - `img_as_*` functions—these would need extra arguments now that range assumptions are no longer available
        - `rescale_intensity` can no longer make range assumptions
        - Have some way of identifying functions that need specifically ints, or need ranges (decorator that registers them, or perhaps even via type annotations)
            - In docs, display list of functions that require ints; suggest user converts input to float
            - Should we have a separate namespace for such functions?

- **MAJOR QUESTION:** Do we warn people over several releases, Twitter, SciPy Tools session, etc, that 1.0 is coming and will have breaking changes, OR, do we use something like Mark's deprecation decorator ([#4464](https://github.com/scikit-image/scikit-image/pull/4464)) to deprecate a massive chunk of the library?
    - Signal via major release version, and via a detailed API transition guide
        - For every error that results from a change, capture how that error looks, and help users to work around it (doc page or notebook)
    - General agreement to move forward, and incorporated the changes proposed:
        - Range checking disabled
        - xy -> rc coordinates
        - strict (safe transition) mode: if function changes behavior in 1.0 (i.e., using the same inputs in 0.X would produce a different result), then raise with instructions explaining what is different, and how to retain the old behavior using the new API. In strict mode, no error is raised when  explicitly providing newly introduced keywords
        - Outstanding API changes
        - Drop some little-used functions; move them to skimage-contrib
        - Should `viewer` submodule move out to own package?

- Threshold API
    - Does it make sense to unify API into `threshold`/`threshold_adaptive`, or move to own submodule? 
    - Single function: do their keywords differ enough that this would be painful to document?

- "Simple namespaces" — duplicate functions where users may expect to find it in API
    - Generally leaning against that notion; users may be confused by funding function in multiple spots, code snippets that differ could do the same thing


- Audit API to ensure consistency across the whole library. e.g.
    - `max_sigma` vs `high_sigma` vs `sigma_max`, `labels` vs `label_image` vs `segmented`, `threshold_otsu` vs `metrics.structural_similarity` & `segmentation.slic`
    - segmentation values including 0 or not
    - using 0 as the default background value in a segmentation vs not
    - regionprops -> return ordered dictionary rather than list

- Any remaining xy -> rc changes
- Change draw to take in coordinate tuples rather than r, c as separate values.
- change our API promise from "we always return numpy arrays" to "we return objects satisfying the array protocol" (ie duck-arrays, and/or things that can be coerced to a NumPy array with `__array__`). How about xarrays?
    - https://github.com/inducer/pyopencl/pull/301
    - It would be also nice to:
        - Support pass-through of duck arrays where possible (most functions that only use NumPy primitives should work)
        - Automatically test and annotate which functions support duck arrays and which don't
    - Example: gputools can accelerate registration (3544) >10x on my laptop, probably closer to 60x if the evaluation function is also made to work with duck arrays.
- Removing the viewer, pointing people to napari instead. Maybe one doc page showing how to visualize images with several libraries? +1
- Removing io, moving all of it to imageio. (Already spoke to Almar about moving imageio to the skimage umbrella.) 
- Discuss type annotations
    - Better support for tools like numba
    - Better control of errors, tests
- Discuss the adoption of Black (resounding NO in the room)
- Extension packs: `scikit-image['data']`, `scikit-image['contrib']`?
- Better tests in the future; Hypothesis?

- API policies in light of, e.g., discussion following https://github.com/scikit-image/scikit-image/issues/3892#issuecomment-590270874
    - An argument `extra`, `extra_output` (or something better) + Union of types (https://docs.python.org/3/library/typing.html#typing.Union) -> returning image, NamedTuple as a possible solution
    - mypy for type checking: http://mypy-lang.org/, https://github.com/python/mypy
    - `extra` would be the same for all API
    >>> from skimage.util import extra
    >>> extra(function)(args)
    - function.extra <- the function with the extra stuff
    - extra decorator: @extra()def func, this creates a new function, func_extra, that has the extra return types.
    - documentation:
    """
    Parameters
    ----------
    (...)
    Returns
    -------
    (...)
    Additional returns
    ------------------
    (...)
    Examples
    --------
    (standard examples go here)
    >>> from skimage.util import extra
    >>> example using extra()
    >>> example using function.extra()
    (...)
    """

#### Unrelated to code

(These are things S suggests can be done for the 1.0 release, not items to be discussed *in this meeting*.)

- Redo website for 1.0 release
    - Show contributors (and add paragraph to say we're actively looking for diverse contributors)
    - Showcase usage in academia / industry
    - Vet documentation language
    - Highlight mission statement
    - Provide options to donate funding
    - Restyle docstring CSS (see if we can work around Sphinx limitations)
    - Consider Hugo?

- Reach out to partners who can help announce 1.0
    - BIDS
    - CZI
    - NumFOCUS
    - Monash
    - Plot.ly
    - ... ?

- Discuss how to improve our interactions with forum.image.sc
    - Suggestion: after every example/tutorial, add a link: "further questions? ask on forum.image.sc"

- Discuss how to better organize development
    - Current mode is fairly haphazard
    - Would be good to have milestones that are worked on in 2–4 week iterations
    - Perhaps every 2nd or 4th community call can be an iteration meeting?
    - Should we break up responsibilities for being communicative on various parts of the project?  Or switch off on being the person that tracks new items for that week, filing it correctly? Emma to send an e-mail on the core-dev mailing list to ask about who could be in the group of people being in charge for one week at a time.
    - Every PR must fix an issue. Don't create a PR without first creating a corresponding issue. <- put this in the contributing guide

- Discuss funding sources to pursue
    - Funding prospectus
        - What do we do
        - Why do we need funding
        - What funding options do you have
        - What work will be sponsored (roadmap)
        - How will funds be managed
    - Two kinds of goals (company sponsor)
        - Specific feature
        - Unrestricted gift / general sponsorship: software is useful to company (harder to get; harder for the company to relate)
    - Potential sponsors
        - Microscopy companies
        - R&D companies: engineering, electricity, microelectronics
        - Aligned to our values
        - Add deep learning doc

- Advertise skimage augmentation of deep learning pipelines better
    - Preprocessing (normalization, rotation, augmentation)
    - Postprocessing (counting labels, )

- In-person sprint to push toward 1.0; then, another to develop post 1.0 roadmap

- Webpage: add pages for core devs and steering council

- On the webpage and documentation tools
    - jupytext: https://github.com/mwouts/jupytext
    - Ross's discussed repos — ipypublish: https://github.com/rossbar/ipypublish, myst_parser: https://github.com/rossbar/myst_parser

- Excellent tutorial from Marianne: https://scikit-image.org/docs/dev/auto_examples/segmentation/plot_regionprops_table.html

## Questions



## Action items


---

After the meeting, please commit the contents of this document into the [meeting notes](https://github.com/scikit-image/meeting-notes) repo. Then clear out this document so that it can be re-used for the next meeting.

