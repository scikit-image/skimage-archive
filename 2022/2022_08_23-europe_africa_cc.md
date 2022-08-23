# scikit-image Community Call

- **Time:** Tuesday, August 23, 17:00 – 19:03 UTC
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**

**Present:** Lars, Marianne, Alex

## Maintenance

### Inactive PR management

- A Kanban board / project like [Inactive PR Management - NumPy](https://github.com/numpy/numpy/projects/16#card-83557887) to manage stalled PRs? 
- Combine with [Stale Bot](https://github.com/marketplace/stale) but with nicer label, e.g. ":sleeping: dormant/inactive"?
- Warning in the middle: is this flying under the radar?
- helps with prorizing more active PRs with active participants
- Not depending on people
- 1st step: using the tag
    - Give a space to discuss that with the other core members
- 2nd step: automatically closing stuff
    - Maybe another tag? "dormant 1 month," "dormant 3 months," "dormant 6 months," "😵 dormant 1 year"
    - If we leave this to the weekly manager, we should specify precisely what the weekly manager should take care of
- Action: post on forum to collect feedback for 1 week, followed by silent consensus (Lars)

### Weird bots acting on skimage?

- Any ideas on what happened here: https://github.com/scikit-image/scikit-image/pull/6470?
	- see https://github.com/scikit-image/scikit-image/pull/6470#issuecomment-1224251748

### Criteria for including new functionality

- https://discuss.scientific-python.org/t/criteria-for-including-new-functionality-into-scikit-image/405/11

### 0.20 milestone

- Is it the current priority? https://github.com/scikit-image/scikit-image/milestone/22

## Education and Dissemination

### Talks at Data Umbrella

- [Data Umbrella's YouTube channel](https://www.youtube.com/c/DataUmbrella)
- Alex will give a talk on Oct 18 ("An overview of 3D image processing using scikit-image").
- Marianne will give a talk on Oct 25 ("A bioimage data analysis workflow with scikit-image").

## Community management

### Changing the frequence of our meetings

- From weekly to biweekly, currently
- Lars is happy with weekly meetings
- Alex will decide

### A better address for our meetings

- We have two new links for our Community Calls, already — thanks NumFOCUS!

### Please keep a lower bar for first contributors

- Extra/massive (late) rounds of reviews take a toll
- If the contribution could be expanded, approve/merge the first PR and ask for a new contribution (we want to _loyalize_ our contributors :slightly_smiling_face:).
    - Always keep the big picture in view
    - Extra work should be optional
    - For maintainers: avoid "Request changes," especially if you're not around to update your review -- They block our PRs! :)
- On git/github: some introductory material from Juanita?
    - We could bring that to our contributors guide
- When people need our help and we can help, please do!

### Rotating on-duty weeks?

- Yes :)

### Inviting other core members to attend to these meetings?

- Some core members are MIA. Should we ping them biweekly to check if they are around?

## Extras

- Lars is working on [Update notebooks for EuroSciPy 2022 #70](https://github.com/scikit-image/skimage-tutorials/pull/70).
    - question related to `active_contour`, which doesn't really fit the astronauts head in [4_segmentation.ipynb](https://github.com/scikit-image/skimage-tutorials/blob/main/lectures/4_segmentation.ipynb)
    - Maybe using this? https://scikit-image.org/docs/stable/auto_examples/edges/plot_active_contours.html
    - Snakes are tricky — mainly, their initial conditions
    - Maybe at some point we could consider: [Gradient Vector Flow: A New External Force for Snakes](https://iacl.ece.jhu.edu/pubs/p087c.pdf)
- Marianne has reached out to a colleague in QLS (Quantitative Life Sciences) to come up possibly with new gallery examples using biomedical images.
    - https://github.com/scikit-image/scikit-image/pull/6469
    - Collaboration with Gus Becker (Materials Science)
    - How does one combine maintenance with new features/tutorials?
