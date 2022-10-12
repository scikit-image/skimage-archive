# scikit-image Community Call

- **Time:** Tuesday, October 11, 17:00 – 18:00 UTC
- **Join via Zoom:** [Europe/Africa](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09) (odd weeks),   [Americas/Oceania](https://us06web.zoom.us/j/89135215899?pwd=ck8xRGg1SVNEWmlGMjlSd1BiOVZtZz09) (even weeks)
- **Notes:** https://hackmd.io/@alexdesiqueira/skimage_cc
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**

**Present:** Lars, Stéfan


## Maintenance

- [Taking part in Closember](https://discuss.scientific-python.org/t/taking-part-in-closember/547)
	- Anything to prepare?
	- Done, we are listed on https://closember.org
- Lars: Confusion about intention behind [milestone 1.0](https://github.com/scikit-image/scikit-image/milestone/9)
	- should every merged PR in 1.0 go into 0.20 and release notes?
	- We renamed the 0.1 milestone to 0.21, and triaged all issues to either (a) stay with 0.21 (b) go to 0.20 (c) go to 2.0 or (d) be cleared / closed. 
- [Add linting via pre-commit #6563](https://github.com/scikit-image/scikit-image/pull/6563)
	- Do we prefer gradual adoption or all at once?
	- Lars: because most tools in pre-commit run on a full file we should do the update at once. I don't want ask contributors to address unreleated complains in a file they are editing
- [Adding black as linter?](https://discuss.scientific-python.org/t/adding-black-as-linter/548/15)
	- next steps to reach a decision?
	- give people time to talk about it more / propose alternatives
- [Add Meson-based build #6536](https://github.com/scikit-image/scikit-image/pull/6536)
  - Working on dev.py tool for skimage
  - Test suite passes
  - Added CI
- [Automatically merging a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/automatically-merging-a-pull-request) is now enabled for our repo
	- e.g. squash and merge once the CI is green without having to wait for it

## Community management

- Why 2 separate Zoom rooms for our community calls?
	- Lars: using one might be less confusing
	- Update our calender and then the template and then delete one of the rooms
- How do we feel about having a moderator keeping an eye on the time and open discussion points?
  - Stéfan: worth having someone lead the meeting
- Idea: [Configure incoming email to create new topics or group messages](https://meta.discourse.org/t/configure-incoming-email-to-create-new-topics-or-group-messages/62977/1) 
	- Lars: This might lower the barrier to get in touch as discuss.scientific-python.org requires an account.
	- Stéfan: We already have an address: skimage@discuss.scientific-python.org
	  - Make sure that is listed in the docs (I think currently we only have URL to forum)
	  - see [Include developer forum email address in documentation #6575](https://github.com/scikit-image/scikit-image/pull/6575)
- Stéfan: Update order of links in issue selection dialog
	- Dev forum, Image.sc, Chat, StackOverflow
	- see [Update order of links in issue selection dialog #6576](https://github.com/scikit-image/scikit-image/pull/6576/files)
