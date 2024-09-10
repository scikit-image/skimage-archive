# scikit-image Community Call

- **Time:** Tue, 2024-08-13, 17:00 – 18:00 UTC
- **[Join video call via Jitsi](https://meet.evolix.org/skimage-meeting)**
- ~~**[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**~~
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**
- **[Code of Conduct](https://scikit-image.org/docs/stable/conduct/code_of_conduct.html)**

**Present:** Stéfan, Lars

## Agenda

### EuroSciPy

- Who's attending?
	- Confirmed: Marianne, Stéfan, Lars, Greg
	- Maybe: Egor? (Lars will reach out)
	- Not: Jarrod

- Tutorial, currently at [mkcor/euroscipy-2024-scikit-image](https://github.com/mkcor/euroscipy-2024-scikit-image)
	- Plan to use JupyterLite
	- Not sure if Pyodide will include recent version by then, but merged [Upgrade scikit-image to 0.24.0 / pyodide#5003](https://github.com/pyodide/pyodide/pull/5003), also Marianne and me are now listed as recipe maintainers
	- Who will present which section:
		- Images as arrays: Marianne
		- Filtering: Lars
		- Segmentation: Stéfan

- Skimage sprint
	- Conference team suggested the [Technopark Pomerania conference centrum](https://technopark-pomerania.pl/o-nas/infrastruktura/centrum-konferencyjne/sala-konferencyjna/view_express_entity/19), it's 30 min out by bus, might get it for free otherwise ~90 EUR/day
	- Preparation going on (agenda will be shared with community!)
	- Any maintainers available remotely? (Lars will ask on forum)

- GPU backend
    - Can we get SSH access to a test machine? Conact Sebastian / Greg.

- Guidelines on async discussions, [being discussed on SciPy list](https://discuss.scientific-python.org/t/guidance-around-in-person-or-synchronous-discussions/1333/2)

### Review opportunities

- [Uncomment currentmodule directive again #7492](https://github.com/scikit-image/scikit-image/pull/7492) minor fix
- [Fix dynamic max trials of RANSAC #7065](https://github.com/scikit-image/scikit-image/pull/7065) needs 2nd approval
- [Add CI to release nightly free-threaded wheels #7481](https://github.com/scikit-image/scikit-image/pull/7481) needs 2nd approval
- [Complete deprecation of plot_matches #7487](https://github.com/scikit-image/scikit-image/pull/7487) needs 2nd approval
- [Refactored tests for skeletonize #7459](https://github.com/scikit-image/scikit-image/pull/7459) needs 2nd approval

(Stéfan will have a look after the meeting)
