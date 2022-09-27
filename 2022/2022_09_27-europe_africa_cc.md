# scikit-image Community Call

- **Time:** Tuesday, September 27, 17:00 – 18:00 UTC
- **Join via Zoom:** 
  [Europe/Africa](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09) (odd weeks), 
  [Americas/Oceania](https://us06web.zoom.us/j/89135215899?pwd=ck8xRGg1SVNEWmlGMjlSd1BiOVZtZz09) (even weeks)
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**

**Present:** Marianne, Lars, Stéfan

## Maintenance

- PR to roll out "dormant" label: https://github.com/scikit-image/scikit-image/pull/6546
- Discussion on "OK to merge" label (also, use filter https://github.com/scikit-image/scikit-image/pulls?q=is%3Apr+is%3Aopen+review%3Aapproved -- maybe bookmark this page)
- Marianne: reply to Lars's question on single/double review/approval when contributor is core dev (in general, the usual rule applies)
- (Stéfan) the rule is that you want two core devs to have looked at the code
- How to generate release notes
    - Could add a fenced code block with release notes, parse it out with a tool like [github-activity](https://github.com/executablebooks/github-activity)
        - See [recent PR](https://github.com/executablebooks/github-activity/pull/70)
	- (Marianne, Lars) just +1'd https://github.com/scikit-image/scikit-image/pull/5477#issuecomment-976087780
	- we need to define categories (new feature, bug fix, etc.)
- Broken math (LaTeX) rendering in docs (Lars found the solution! Add a space between '..' and 'math') https://github.com/scikit-image/scikit-image/issues/6547
- Review work for https://github.com/scikit-image/scikit-image/pull/6462 (+ discussion at https://discuss.scientific-python.org/t/is-the-algorithm-on-division-of-self-overlapping-polygons-a-good-fit/501)
- Discussion of pathway to skimagev2: should we be getting community input on whether we should take that route? What is the cost of SKIP4, or some of the routes in SKIP3 (advertising via version numbers/docstrings/release notes). What can we get away doing without skimage2?

## Community management

- Consider communicating in Basic English: https://simple.wikipedia.org/wiki/Basic_English
    - (Lars and Marianne) we don't know who made this suggestion
    - (Stéfan) answer: it was Alex 
    - we are not targeting a general audience
    - it's challenging enough to put something complex into words, what if we have to limit ourselves to fewer words (i.e., 800 words!)...
    - Might be relevant as a soft goal in our documentation (which part of the documentation?)
    - we speak "scientific English" anyway, not Shakespearean English
    - (Marianne) as contributors, we want to *grow* and, hence, the goal isn't to go for the lowest common denominator...
    - (Stéfan) avoid technical jargon and pompous language, obviously; not sure basic English always simplifies communication for communities who share common understanding of certain topics (think of explaining complex natural phenomena)
- Add emojis to [weekly report](https://github.com/scikit-image/boilerplate-utils/blob/main/skimage_weekly_update.py) to indicate the PR or issue state (and tags?): e.g., closed 🤝, open 🙌?
