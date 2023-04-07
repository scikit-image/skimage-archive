# Tuesday, June 28, 10:00 – 11:00am Pacific

**- [scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
**- [Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**

**Present:** Lars, Greg, Alex

## Topics

### SciPy '22 sprint

* July 16–17, 2022
* Alex thinks it should be virtual, on [Discord: Mentored Sprints](https://discord.gg/EvmCVQ3xTU) 
    * Structure is already there:
![](https://i.imgur.com/sgdMFad.png)
    * A bunch of us are there, too (Greg, Marianne, Juan at least)
    * If sprints can't be virtual, they can be... coincidental (rogue :wink:)

### Moving the website to Scientific Python's theme?

* Proposed this to Stéfan a while ago:
    * _"1. Maybe it's time for us to adopt the scipyeco theme? Now that I'm seeing the issue I closed (https://github.com/scikit-image/skimage-tutorials/pull/59) and the one Ross is working on (https://github.com/scikit-image/skimage-tutorials/pull/66) on skimage-tutorials, I don't think that's the way to go; I feel we should keep that repo as is, to reuse that material in future tutorials, and repurpose/re-add the tutorials there as documentation, or cookbooks. By the way, ..._
    * _2. We should have cookbooks! 🙂_"
        * S: Curious why you don't think we should accept #66. I'd have preferred a less magical build system, but it does seem to take us in the direction we discussed before.
* Using numpy's layout as an example: ![](https://i.imgur.com/6RFm1b1.png)
* https://theme.scientific-python.org/
* https://github.com/scikit-image/skimage-tutorials/ should be a part of the website

### Every PR should fix an issue

* From the [scikit-image developer hackathon, BIDS, 2020-02-{27,28}](https://github.com/scikit-image/meeting-notes/blob/main/2020/2020-02-27--BIDS-core-dev-meeting.markdown): _"Every PR must fix an issue. Don't create a PR without first creating a corresponding issue. <- put this in the contributing guide"_
  * S: Why? If a PR has a good description of what it changes, that should be as good as an issue?
  * A: to avoid rework/lost work from our contributors; transforms/functions/improvements are implemented but not seen/reviewed and go stale, generating rework/lost work for the contributor
* Opens up a space for discussion (why is this feature/improvement important? Where does it come from?)
* Saving contributors from lots of lost work and PRs we don't fully understand

### Close Zulip, open Discord?

* Maybe useful for us (maintainers and friends) to have a quick-comm channel in Scientific Python's Discord, instead of Zulip?
  * S: Should be no problem to give skimage regular contributors access there, but will probably not make SP discord open to anyone from the public. Maybe encourage questions to go to the forums anyway?
* A part of the ecosystem is starting to adhere; less rework, trying to centralize things 🙃️ 

# Discussed

* Greg: SciPy slide for skimage update
* skimage 1.0 release [(SKIP4)](https://scikit-image.org/docs/dev/skips/4-transition-to-v2.html), [1.0 Milestone](https://github.com/scikit-image/scikit-image/milestone/9)
    * Be careful to not merge any incompatible API (skimage 1 vs 2)
    * Maybe prepare project page to highlight last remaining steps
* skimage 2.0
	* Juan suggested to refactor graph module?

