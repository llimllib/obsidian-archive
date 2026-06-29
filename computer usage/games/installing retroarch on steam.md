---
created: 2026-06-29T00:14:02.301Z
updated: 2026-06-29T00:14:02.301Z
---
- Retroarch gets installed to `~/Library/Application\ Support/Steam/steamapps/common/RetroArch`
- I had to disable the PS5 button support in mac to get it to work inside retroarch
	- Retroarch also picked up my controller as #2 instead of #1, and I had to flip it in settings
	- I had to disable the steam overlay to get the ps5 button working in retroarch
- guide [here](https://steamcommunity.com/sharedfiles/filedetails/?id=2929236360) telling you how to get the cores, which are not built in
	- doesn't work on OS X though
- steam has some DLC cores, so I installed the Beetle PSX DLC
	- that got close to working! But then it failed on the firmware, so need to figure out what dir to install it to
	- `cp SCP* ~/Library/Application\ Support/Steam/steamapps/common/RetroArch/system`
		- got it going