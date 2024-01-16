# scikit-image Community Call

- **Time:** Tuesday, January 16, 2024, 17:00 – 18:00 UTC
- !!!Apparently unavailable!! ~~**[Join video call via Jitsi](https://framatalk.org/skimage-community)**~~ Let's use Zoom for now
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Marianne, Lars, Stéfan (joined late)

## Agenda

- Lars: preparing for NumPy 2.0 in [Test nightly wheel build with NumPy 2.0 #7288](https://github.com/scikit-image/scikit-image/pull/7288)
  - We rely on removed `np.lookfor`. Do we skip deprecation cycle, [vendor it](https://github.com/scikit-image/scikit-image/pull/7288#discussion_r1451033431) or something inbetween..?
  - Can I release 0.22.1 with NumPy<2.0 bound? -> Ask Jarrod to chime in
  - [NEP 50](https://numpy.org/neps/nep-0050-scalar-promotion.html) changed promotion rules, somewhat tricky to figure out

- Albert Steppi reached out: [Localization of scikit-image website content. #7296](https://github.com/scikit-image/scikit-image/issues/7296)
  - Prioritize [Upgrade to hugo and Scientific Python theme #94](https://github.com/scikit-image/skimage-web/pull/94)
      - Lars will get into building state, and Stéfan will develop missing components

- Conferences
  - [SciPy 2024](https://www.scipy2024.scipy.org) is Jul 8-14 in Tacoma, proposal deadline: Feb 27, 2024
