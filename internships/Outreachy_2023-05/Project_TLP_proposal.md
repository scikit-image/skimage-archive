# Outreachy proposal on `transform` module and thin-plate splines

References:
- Feature request: [2D image warping via thin-plate splines #2429 - github.com](https://github.com/scikit-image/scikit-image/issues/2429)
- Paper: [Bookstein, Fred L. "Principal warps: Thin-plate splines and the decomposition of deformations." IEEE Transactions on pattern analysis and machine intelligence 11.6 (1989): 567-585.](http://user.engineering.uiowa.edu/~aip/papers/bookstein-89.pdf)
- [Simple implementation from Zachary Pincus - github.com](https://github.com/zpincus/celltool/blob/master/celltool/numerics/image_warp.py)
- [image.sc thread](https://forum.image.sc/t/equivalent-for-matlabs-piecewiselineartransformation2d/51035/4) discussing related transforms and Zachary's implementation
- [Registration and warping - Project on github.com](https://github.com/scikit-image/scikit-image/projects/8)

----

## Project Info

### Project Skills
| Skill description  | Impact on intern selection | Experience Level |
|--------------------|----------------------------|------------------|
| Image processing   | Preferred                  | 2 (Concepts)     |
| Array programming  | Preferred                  | 3 (Experimented) |
| Python programming | Preferred                  | 4 (Comfortable)  |

### System Requirements
The intern will need one of the following platforms:
- Windows 64-bit on x86 processors
- Mac OS X on x86 / Apple Silicon / M1 / M2 processors
- Linux 64-bit on x86 processors

### Project Description

**Title:** Enhance image warping in scikit-image with thin-plate splines

scikit-image is a Python library for image processing with scientific focus. Its transform module provides a set of algorithms to warp and transform images or volumetric data. These are used in feature detection, image alignment, data compression, modelling, or to correct distortions in fields such as medical imaging, geology, and machine learning.

The focus of the internship is to add a new image warping function using thin-plate splines (TPS) to scikit-image. TPS can be imagined as if bending a thin plate smoothly between two sets of points. This deformation can be interpreted as a warped image when viewed from a 2-dimensional perspective. The method is flexible, reliable, and produces a smooth, continuous transformation that preserves the local shape of the image. These properties are useful in many applications and would be a great addition to the toolkit of scikit-image's users.

Candidates may be self-taught, hold or be completing a BSc in Computer Science, Applied Math, or another computational discipline (or equivalent). Experience and/or interest in open-source software, scientific data analysis, image processing, and/or technical writing are very welcome.

### Internship Tasks
Foremost, the internship is meant as a learning experience for the intern, and mentors will try to adjust tasks to the strengths and skill level of the intern.

In the beginning, the mentor (and co-mentor) will provide the intern with several resources, starting points and smaller tasks. These might involve related issues in scikit-image’s transform module, or tasks to get familiar with the project’s infrastructure and important concepts. Self-initiative and new ideas by the intern are of course very welcome.

Once accustomed, a new warping function based on thin-plate spines could be implemented and added to scikit-image. A [prototype implementation of the algorithm already exists in Python](https://github.com/zpincus/celltool/blob/8d7a2b778cd45cf91588451f7f3c4784b049a82c/celltool/numerics/image_warp.py) and may be taken as a starting point. Together with mentors and the community, the intern will design an API for the implementation that is consistent with the transform module and create tests ensuring its correctness.

Depending on the progress during the internship, the intern may also optimize the performance of the algorithm and create a new tutorial or gallery example for the new function.

### Intern Benefits
The intern will experience the end-to-end process from conception of a new idea to its integration into an existing API. With the help of mentors and the community, the intern may expand their skill set in a wide range of concepts and technologies. This will involve API design, code maintainability, performence optimization, and effective collaboration on these things. 

Apart from personal improvement, the intern will also engage with and become part of a welcoming, skilled, international and science focused community that values openness, collaboration and diversity. The mentors and the scikit-image team would be very happy to see new opportunities develop following the internship.

### Community Benefits
This project will add a robust, flexible and requested warping algorithm to the scikit-image and in extension make it available to a wide community of scientists and Python users. This, and smaller tasks that are part of the internship, will also benefit the codebase and scikit-image and in general. It is the hope of the scikit-image team, that this internship will be an entry point for a new member of the open source community.

### Project Contribution Information
As part of the application process, all applicants must make at least one contribution to be accepted as an intern for this project. Only applicants who make a contribution will be eligible to be accepted as interns. This community requires applicants to complete a tutorial before they can make their contributions.

Please build your development environment by following these instructions: https://scikit-image.org/docs/dev/contribute.html

Applicants can contribute to this project through [the project repository or contribution page](https://github.com/scikit-image/scikit-image). The project uses an [issue tracker](https://github.com/scikit-image/scikit-image/issues) to keep information about bugs to fix, project features to implement, documentation to write, and more. Applicants can look for newcomer-friendly issues to use for their first contributions by looking for the following issue tags in the [project issue tracker](https://github.com/scikit-image/scikit-image/issues): 🔰 Good first issue

During the application period, candidates should start by reading the [Contribution guide](https://scikit-image.org/docs/dev/contribute.html), followed by setting up a local development environment. Following that, several smaller contribution tasks can be chosen to work on:

- Extend incomplete or very terse docstrings. This could include adding or extending the examples section of functions, or more detailed parameter descriptions. Candidates may look for terse docstrings themselves or choose from these lists (please pick only one item of each issue):
  - [Add docstrings to every submodule in skimage #6761](https://github.com/scikit-image/scikit-image/issues/6761)
  - More advanced: [Add short examples to transform classes #6808](https://github.com/scikit-image/scikit-image/issues/6808)
- Choose an [issue tagged as “Good first issue”](https://github.com/scikit-image/scikit-image/issues?q=is%3Aopen+is%3Aissue+label%3A%22%3Abeginner%3A+Good+first+issue%22) to work on.
- Participate in issues and pull requests that have been recently active, especially those of other Outreachy applicants. The goal here is just to get familiar with the interface, the development and review process. Constructively asking for clarification if a description, implementation or documentation is hard to follow can be a very valuable contribution!

Candiades are welcome to introduce themselves in scikit-image's [Outreachy topic on Zulip](https://skimage.zulipchat.com/#narrow/stream/176555-sprint/topic/Outreachy). Mentors and other library maintainers will monitor this chat room and are happy to help with any questions that may arise.

### How do I work with the scikit-image community?
Outreachy applicants can get help and feedback from both mentors and community members. Community members discuss their contributions in a public chat. Outreachy applicants can often learn from those discussions.

Please introduce yourself on the public project chat:

- **Zulip** - You can find helpful documentation about this communication tool [here](https://zulip.com/help/). Once you join the project's communication channel, the mentors have some additional instructions for you to follow:
  Feel free to ask any questions here. This is probably our most informal and chat like communication channel. If you are posting, please look for the most fitting stream and topic. In case of Outreachy related things that will probably be the [topic "Outreachy" under stream "sprint"](https://skimage.zulipchat.com/#narrow/stream/176555-sprint/topic/Outreachy).
  [Follow this link](https://skimage.zulipchat.com/) to join this project's public chat.
Log in with GitHub or create a new account. Join topic ["Outreachy" under stream "sprint"](https://skimage.zulipchat.com/#narrow/stream/176555-sprint/topic/Outreachy). Please introduce yourself and post there! You are welcome to tag your mentor (Lars Grüter @lagru) or send him a private message if you have questions.
- **Developer forum** - You can find helpful documentation about this communication tool [here](https://meta.discourse.org/t/discourse-new-user-guide/96331). Once you join the project's communication channel, the mentors have some additional instructions for you to follow:
  This is a good place for longer-form discussions, project-wide topics, decision making and more general discussion of contributions. Before creating a topic here, please search for similar or related ones first and create it in "Contributor & Developer discussion" » "scikit-image" or another appropriate category.
  [Follow this link](https://discuss.scientific-python.org/c/contributor/skimage/22) to join this project's public forum.
Log in with GitHub or create a new account. Feel welcome to tag your mentor (Lars Grüter @lagru) or send him a private message to introduce yourself and ask questions.

- **GitHub** - You can find helpful documentation about this communication tool [here](https://docs.github.com/en). Once you join the project's communication channel, the mentors have some additional instructions for you to follow:
  This is scikit-image's most formal communication space. We aim to keep issues, pull requests and comments focused on the specific development task at hand and on topic. Before creating a new issue or pull request here, please search for similar or related ones first. If in doubt whether post a topic here, you are very welcome to ask on our other communication channels first (Developer forum, Zulip). Also, feel free to tag your mentor (Lars Grüter @lagru) at anytime.
  [Follow this link](https://github.com/scikit-image/scikit-image) to join this project's public repo.

Outreachy mentors will often be in the community public chat. The project mentor's usernames are: mkcor, lagru,

### Mentor experience (@lagru)

> 1. *Has the mentor participated in Outreachy before?*

No, I have never mentored before

> 2. *What is the contributor's mentorship style (how do they expect to interact with accepted interns)?*

An asynchronous and open communication style via scikit-image's established channels (GitHub, developer forum, emailing, messaging) is preferred. A weekly, structured meeting (video-conferencing) should be part of the regular mentor-intern communication. The mentor is willing to pair program with the intern and happy to work together on a specific issue. Asking for help and sharing thought processes and problems is very much encouraged.
    
> 3. *How long has the mentor been a contributor to the team that the intern will be working with (e.g. the team of contributors for a particular subsystem, application, module, documentation team, user experince team, graphical design team, etc)?*

The mentor has contributed to this team for more than 2 years

> 4. *What contributions has this mentor made to the team or other FOSS communities?*

The mentor has been a core-developer for scikit-image for more than 2 years and contributed reviews, bug fixes, new features, general maintenance, helped with community management, funding proposals and participated in discussions. He also contributed to other packages in the scientific Python ecosystem, e.g. NumPy and SciPy among them. During that time his emphasis has been on peak finding, API design, optimization and maintenance.

### Mentor experience (@mkcor)

> 1. *Has the mentor participated in Outreachy before?*

No, I have never mentored before

> 2. *What is the contributor's mentorship style (how do they expect to interact with accepted interns)?*

I prefer async, informal communication during the week (messaging, emailing, comments on GitHub) and a longer, structured meeting once a week (video-conferencing). I am willing to pair program with the intern; I'm happy to work together on specific issues.
    
> 3. *How long has the mentor been a contributor to the team that the intern will be working with (e.g. the team of contributors for a particular subsystem, application, module, documentation team, user experince team, graphical design team, etc)?*

The mentor has contributed to this team for more than 2 years

> 4. *What contributions has this mentor made to the team or other FOSS communities?*

I've been taking care of the overall package maintenance (reviewing pull requests, supporting users, triaging issues, fixing bugs, ...). I have written most of the long-form gallery examples which are based on scientific applications.
