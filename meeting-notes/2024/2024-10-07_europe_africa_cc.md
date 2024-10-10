# scikit-image Community Call

- **Time:** Tue, 2024-10-07, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**


**Present:** Sebastian Berg, Lars Grüter \
**Reviewed by:** Lars Grüter, Stéfan van der Walt (2024-10-09)

## Agenda

- [Inquiry About Deploying scikit-image Website in China #7559](https://github.com/scikit-image/scikit-image/issues/7559)
  - Blogger reached out to us offering to mirror our website for their community including translations
  - Feedback on SP discord is that GitHub's servers can make problems from inside China, we are hosting on GitHub
  - Course of action? 
    -> Lars to escalate to Scientific Python as a cross-project issue

- [Basic infrastructure for dispatching to a backend #7520](https://github.com/scikit-image/scikit-image/pull/7520),
  - Tim asks how to proceed
  - Do we wait for feedback on Aditi's SDG application?
  - -> Have dedicated and **prepared** meeting between invested parties

- Apply to [NIH RFA-OD-24-010 grant](https://grants.nih.gov/grants/guide/rfa-files/RFA-OD-24-010.html) for scikit-image?
  - Letter of intent: December 4 minus 30 days
    Submission: December 4, 2024 (earliest submission Nov 4th)
  - Stéfan is planning to form a team to submit on behalf of skimage, with Berkeley as "host" institution; please let him know if you are interested
  - What the status? -> Stéfan started the process with Berkeley

- [Fix several watershed issues (off-center markers, watershed_line) #7071](https://github.com/scikit-image/scikit-image/pull/7071)
  - Do we want this in 0.25? I can probably update the release note(s) and merge.

- **Review coordination**
  - [Render paragraphs in dormant message #7549](https://github.com/scikit-image/scikit-image/pull/7549), minor tweak (merged)
  - [Feature/enhance plot matched features #7541](https://github.com/scikit-image/scikit-image/pull/7541), waiting for 2nd approval
    - Add cycle example to docstring
  - Anything else...?
