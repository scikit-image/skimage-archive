# scikit-image EOSS5 full application

# Proposal details

## 0. 

## 1. Proposal title: From library to protocol: scikit-image as an API reference

## 2. Previous funding

Did you previously apply for funding for this or a related proposal under the CZI EOSS program?

- Yes

## 3. Proposal purpose

#### Describe the purpose of the proposal in one sentence (maximum 200 characters):

- *Example: To develop a comprehensive, validated atlas of the human kidney at single-cell resolution open to the entire scientific and clinical community.*

To create a consistent, typed-annotated, discoverable, and extensible API for scikit-image and facilitate interoperability in the broader image analysis ecosystem.

## 4. Amount requested

$200K/y for 2y

## 5. Proposal summary

*Provide a short summary of the application (maximum of 500 words) (auto-filled from LOI; update if needed)*

Scikit-image is among the most popular image processing frameworks for scientific image analysis. This proposal aims to support its contributors and maintainers with
- a formalization and typing of scikit-image's API;
- ongoing maintenance and community-driven improvements; and
- mentoring and supporting diverse contributors.

### New typed API and protocols

Scikit-image's popularity can be attributed to its first-class support for n-dimensional NumPy arrays. This support gave scikit-image seamless interoperability with the core scientific Python libraries of not just NumPy itself, but also SciPy, scikit-learn, networkx, and others, enabling users to rapidly create custom analyses drawing from many different scientific libraries.

However, specialized array formats have proliferated for specific needs such as deep learning (PyTorch, TensorFlow), general purpose GPU computing (CuPy, PyOpenCL), and out-of-core and distributed computing (Dask, zarr). The communities that grew around each of these formats came together to define a common [Array API] (application programming interface), allowing users to easily transition between array formats without having to rewrite code.

This proposal aims to do the same for image analysis libraries.

Thanks to its popular position in the ecosystem, scikit-image is already seen as a "standard" API for the community to emulate. For example, NVIDIA's cuCIM library provides a `cucim.skimage` module that emulates the scikit-image API for CuPy arrays. However, since scikit-image grew organically from the contributions of a broad community -- almost 500 direct code contributors -- API inconsistencies exist. Rather than perpetuate these throughout a broader ecosystem, we want to (1) formalize protocols and types for image analysis, and (2) reorganize and annotate scikit-image's API accordingly. With this, we aim to provide a reference implementation that can be easily extended by other libraries, thereby benefiting usability, discoverability, performance, and community innovation.

[Array API]: https://github.com/data-apis/array-api

### Maintenance

Like similar-sized open source projects, scikit-image requires ongoing maintenance to stay up to date with its dependencies, fix newly-discovered bugs, implement new features requested by the community, and make improvements where the API is confusing. A portion of the maintainer time supported by this grant will be spent addressing open issues, pull requests, and other contributions, and performing other general maintenance tasks such as regular community meetings.

### Mentoring

We have always aimed to foster a welcoming environment at scikit-image and were thrilled to see that interactions on GitHub score very highly on positivity and gratitude metrics compared to similar projects ([Paxton et al, 2022]).

In our experience, however, that has been insufficient to grow the community, particularly the maintainer community. Indeed, the paper suggests that *constructive criticism* correlates with contributor retention more than mere positivity. This might be because *learning* is such an important part of the value that contributors derive from open source communities.

Therefore, we propose to focus on outreach, mentoring, and organizing code sprints, as a way to onboard new contributors from diverse backgrounds. We also propose to create paid internships, ideally in partnership with organizations like [Data Umbrella] and [Outreachy], to encourage new contributors to join our team.

[Paxton et al, 2022]: https://onlinelibrary.wiley.com/doi/10.1111/cogs.13134
[Data Umbrella]: https://www.dataumbrella.org
[Outreachy]: https://www.outreachy.org

## 6. Work Plan

*A description of the proposed work for which funding is being requested, including resources the applicants will provide that are not part of the requested funding. For software development-related work (e.g., engineering, product design, user research), specify how the work fits into the existing software project roadmap. For community outreach related activities (e.g., sprints, training), specify how these activities will be organized, the target audience, and expected outcomes (maximum of 750 words)*

### Alignment with existing roadmap

Community education and inclusiveness are part of our [mission and values statement]. 

We have aimed for some time to develop a more consistent API for our community, again as stated in our [mission and values statement]. We have spent a long time gathering community consensus through [SKIP-3] and [SKIP-4].

### Community outreach and mentoring

We will fund two Outreachy fellowships each year of the grant. This will allow interns to work in pairs and support each other, in addition to the mentorship from the scikit-image maintainers.

We will work with Data Umbrella and related organizations to effectively organize sprints that help us grow the community and retain contributors from diverse backgrounds, while supporting their careers through mentoring, teaching, and direct support. We will generally prefer online events, which have been shown to attract more diverse participants, but may organize in-person events where it makes sense (e.g. attached to a conference such as EuroSciPy and offered in conjunction with travel grants).

### Description of typed API work

The benefits of a consistent, type-annotated API extend beyond guidance and documentation. Some benefits we hope to achieve with this project are:

- the scikit-image API will be more easily *discoverable*. For example, in the current API `skimage.segmentation` contains segmentation functions (in the sense of converting images to labels), but also helper functions, and contour segmentation functions (converting "images" to "polygons"). Users cannot know without extensive reading that `segmentation.slic` and `segmentation.watershed` do one type of task, but `segmentation.active_contours` and `segmentation.clear_borders` do entirely different things. Protocols enable users to more quickly discover alternative approaches for their work.
- scikit-image will become more easily extensible: other libraries can provide their own implementations of particular function classes, which can then be discovered by scikit-image and unified in a single namespace. This will drive innovation and help users find even more potential solutions.
- projects like [napari], which aim to make image analysis accessible to non-coders, can display related functions from not just scikit-image, but other libraries that implement its API. This benefits users who get access to consistent but diverse implementations.

A typed API allows us to clearly define what a "segmentation function" is (something that turns "image" arrays into "labels" arrays), or what a labeling function is (something that turns "boolean mask" arrays into "labels" arrays). Then, libraries can implement such functions, and we can discover them, and dispatch to the most appropriate implementation. For example, cuCIM has labeling on the GPU, dask-image has labeling on distributed arrays, and scikit-image has labeling on in-memory arrays. This dispatching requires a strong type annotation system: lacking type annotations, core developer Greg Lee was forced to implement dispatching functions to the GPU based on text mining function docstrings!

Indeed, we have been aiming to implement these type annotations for some time. However, in addition to the extensive, ongoing work involved in gathering community consensus, it turned out that the still-evolving Python type annotation system was not yet expressive enough for our purposes. This is now changing with PEPs [544] (Protocols/Structural Typing), [593] (Flexible Function and Variable Annotations), and [646] (Variadic Generics).

Thanks to PEP-593, we can annotate different NumPy arrays as follows:

```python
from typing import Annotated

ImageData = Annotated[np.ndarray, 'image']
LabelsData = Annotated[np.ndarray, 'labels']
CoordsData = Annotated[np.ndarray, 'coordinates']
```

This then allows us to annotate functions as follows:

```python
def watershed(image: ImageData, ...) -> LabelsData:
    ...

def local_maxima(image: ImageData, ...) -> CoordsData:
    ...
```

With PEP-544, we can describe a `SegmentationFunction` protocol:

```python
from typing import Protocol

class SegmentationFunction(Protocol):
    def __call__(image: ImageData, *args, **kwargs) -> LabelsData:
        ...
```

which enables us to discover functions that match that protocol, and present them in graphical user interfaces such as [napari], and dispatch to appropriate functions for each array input.

The above presents a flavor of how we are thinking about these things. There remain many limitations and details to work out, which we hope will be supported by this proposal. For example, we need an `Array(Protocol)` class that codifies the currently *informal* (documentation-only) array API protocol, to annotate functions as compatible with *any* type satisfying the Array API. And we need to ensure that type checkers like MyPy properly understand `Annotated`, and that `Annotated` can be composed with Variadic Generics and Protocols. We hope to work through these issues with the broader community, including through direct support of community members if required.

[mission and values statement]: https://scikit-image.org/docs/stable/values.html
[SKIP-3]: https://scikit-image.org/docs/stable/skips/3-transition-to-v1.html
[SKIP-4]: https://scikit-image.org/docs/dev/skips/4-transition-to-v2.html
[544]: https://peps.python.org/pep-0544/
[593]: https://peps.python.org/pep-0593/
[646]: https://peps.python.org/pep-0646/
[napari]: https://napari.org

## 7. Milestones and Deliverables

*List expected milestones and deliverables, and their expected timeline. Be specific and include where possible any goals for metrics the software project(s) are expected to reach upon completion of the grant. Please use a third-person voice (maximum of 501 words).*

The step-wise exploration, development and finally formalization of a typed API is critical to enable feedback and draw on the experience of the scientifc community along the way. Therefore, the following milestones are proposed:

- Fully type a submodule of scikit-image as a proof of concept (6th month).
- Provide a standalone image-focused typing module usable by third-party libraries (6th month)
- Propose a draft and outline of a new typed API and protocols to the community (12th month).
- Propose a SKIP (scikit image enhancement proposal) that details a fully typed API and protocols for scikit-image (18th month).
- Full implementation of the SKIP (24th month).

Progress on maintenance or mentoring can be difficult to quantify. However, we aim for the following metrics as indicators of our success in that regard:

- Provide an initial response and triage to all new issues and pull requests within the first week (maintenance, mentoring).
- Provide follow-up to new activity on pull requests within the first week (maintenance, mentoring).
- Resolve at least 50 issues and merge or close 50 pull requests per quarter (maintenance).
- Hold regular community meetings at least twice a month. We will explicitly encourage participation and questions by new contributors (mentoring).
- Offer two paid and mentored interships each year (mentoring).
- Organize two shared programming sessions or sprints each year (mentoring).
- Add 2-4 new maintainers by the end of the two years (mentoring).

## 8. Existing support

*List active and recently completed (previous two calendar years) financial or in-kind support for the software project(s), including duration, total costs in USD, and source of funding. Include any previous funding for these software projects received from CZI outside of the EOSS program (maximum of 250 words).*

scikit-image received funding from CZI under EOSS-1 ($227,500 USD) and EOSS-3 ($210,000 USD).

Juan Nunez-Iglesias is supported by a CZI Imaging Software Fellowship covering work on scikit-image but also the broader scientific Python imaging ecosystem. The first year of work was focused on scikit-image, but increasingly his time has been taken up working on napari.

## 9. Landscape analysis

*Describe the other software tools (either proprietary or open source) that the audience for this proposal primarily uses. How do the software project(s) in this proposal compare to these other tools in terms of user base size, usage, and maturity? How do existing tools and the project(s) in this proposal interact? (maximum of 250 words). (auto-filled from LOI; update if needed)*

scikit-image is the most commonly used Python package in biomedical imaging, with almost 5M downloads per month from PyPI. (Note that these numbers are inflated by continuous integration systems, but they should be able to provide a point of comparison between libraries.) OpenCV receives roughly the same amount, but, because many of its routines are 2D-only, its usage is less common in biomedical research. By contrast, simpleITK gets 110,000 downloads per month, ITK (see below) 50,000, Mahotas 15,000.

The closest software in the ecosystem is probably the insight toolkit (ITK). ITK is a C++ library that provides Python bindings. Its object-oriented API is constrained by its C++ basis, which makes it less intuitive for Python users. However, its C++ origins also provide strong typing, which means that they have a leg up on scikit-image in terms of strong typing. We will take strong inspiration from the ITK type hierarchy when thinking about scikit-image protocols. Similarly, we will draw from ImageJ2, a next-generation Java-based image processing tool with a strongly typed API around which a large plugin ecosystem has been established.

Other packages are emerging that we aim to support with this proposal, including PyClesperanto, a library that uses OpenCL to perform very fast image processing on any GPU, CuCIM, a library using CUDA to do the same only on NVIDIA GPUs, and dask_image, a library that uses dask to perform image processing on very large arrays, potentially in distributed computing environments.

## 10. Value to biomedical users

*Describe the expected value of the proposed work to the biomedical research community (maximum of 250 words). (auto-filled from LOI; update if neeeded)*

The biomedical community is the biggest community of scikit-image users, based on citations to the scikit-image paper (13 of the 20 most recent citations on Google Scholar were from biomedical research, out of all the sciences). This can be attributed to our strong support of n-dimensional image processing and analysis, which is very useful in bioimaging, where volumetric imaging and volumetric time series are common.

All these users use the scikit-image through its Python API. That is, scikit-image currently serves (by and large) only Python users. Establishing a set of scikit-image types and protocols will allow plugins to develop around it, and programs like napari will be able to automatically generate user interface elements not only for scikit-image itself (a goal since the early days of napari!), but also for a whole ecosystem of libraries implementing scikit-image protocols.

Doing this will open up scikit-image *directly* to users who don't know Python, which represents a large percentage of the biomedical research community.

## 11. Category

1 - Imaging
2 - Data management and workflows

## 12. DEI Statement

*Advancing DEI is a core value for CZI, and we are requesting information on your efforts in this area. Describe any efforts the software project(s) named in this proposal have undertaken to increase diversity, equity, and inclusion with respect to their contributors and audience. Please see examples from applications funded in previous cycles (maximum of 250 words)*

As described in our project summary, we have aimed to create a welcoming and inclusive environment in our project, and felt validated in our efforts by the recent study by [Paxton et al, 2022]. However, we have recognized that this is not sufficient to help diverse contributors join our community, as they may be held back from contributing by structural and systemic barriers.

It is therefore important to directly support the careers of diverse participants and enable their participation in open source communities. (We note that in the past two rounds, key personnel supported in this project by EOSS were women.)

That's why a core focus of this proposal is the mentoring and support of new and existing contributors, especially those who might not otherwise have a chance to contribute to open source. As maintainers, we can provide guidance and learning opportunities that reach internationally. CZI support would both enable that work and enable us to provide paid internships and other support (such as travel to a SciPy conference) that advances the careers of diverse participants. 
