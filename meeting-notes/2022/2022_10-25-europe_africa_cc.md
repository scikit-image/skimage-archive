# scikit-image Community Call

- **Time:** Tuesday, October 25, 17:00 – 18:00 UTC
- **[Join video call via Zoom](https://us06web.zoom.us/j/88060567580?pwd=THRpaWFnSFNwK0Fycy9FVk5RYnV5UT09)**
- **Notes:** https://hackmd.io/@scientific-python/HJWUBDVNi
- **[scikit-image Community Calendar](https://scientific-python.org/calendars/skimage.ics)**
- **[Archive — Meeting Notes](https://github.com/scikit-image/meeting-notes)**

**Present:** Lars, Stéfan

## Maintenance

- [Add Meson-based build #6536](https://github.com/scikit-image/scikit-image/pull/6536)
  - After some last tweaks, waiting for PR to go green
  - Stéfan: Will add `dev.py` after merge to make build process easier
- Release 0.20
	- [0.20 milestone](https://github.com/scikit-image/scikit-image/milestone/22), ~39 open items
	- Whittled down to 21
	- Pending removal, unless they receive attention:
	  - https://github.com/scikit-image/scikit-image/pull/6493
	  - ...
	  - will review remaining items more closely and either resolve them or push them to 0.21
	- [Prepare release notes for v0.20.0 #6556](https://github.com/scikit-image/scikit-image/pull/6556), ready for review
	- [Complete deprecations targeting release 0.20 or 1.0 #6583](https://github.com/scikit-image/scikit-image/pull/6583), ready for review
	- Lars: unsure how to resolve this https://github.com/scikit-image/scikit-image/pull/6583#discussion_r998259177
		- Stéfan: Need another None-proxy, e.g.:
      ```python
      class NoChannelAxis:
          pass

      def gaussian(..., channel_axis=NoChannelAxis):
        if channel_axis is NoChannelAxis:
            ...

      # User can do:
      gaussian(..., channel_axis=None)
      ```
- [Are lpi_filter, ridges and forward_filter part of our public API? #6593](https://github.com/scikit-image/scikit-image/issues/6593), easy fix after decision


## Community management

## Education and Dissemination
