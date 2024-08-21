---
updated: 2024-08-21T13:01:35.398Z
created: 2023-10-20T13:54:09Z
---
https://saurabhs.org/advanced-macos-commands

- `caffeinate` - set Mac sleep behavior
- `textutil` - document file converter
- `mdfind` - search with Spotlight
- `networkquality` - measure Internet speed
- `screencapture` - take screenshots
- `pbcopy`, `pbpaste` - interact with system clipboard
- `taskpolicy` - control scheduling of processes
- `say` - text-to-speech engine
- `sips` - image manipulation
- `open` - open files and applications
- `pmset` - configure power management
- `networksetup` - configure network settings
- `qlmanage` - manage Quick Look
	- convert an svg to a png:
		- `qlmanage -t -s 1024x1024 -o MyIcon.iconset/Icon1024.png icon.svg`
	- with a caveat from a news.yc reader that sometimes the svg renderer isn't perfect
- `softwareupdate` - manage OS updates

most I knew, but a few I didn't! handy resource

the [news.yc](https://news.ycombinator.com/item?id=36491704#36492924) comments mention:
- `hdiutil` as well, which I've used, to mount and unmount volumes
- which is actually different from `hidutil`, which you can use to remap keyboard keys! 
	- (I use [[karabiner]]) (also mentions for this [web app to generate the appropriate input](https://hidutil-generator.netlify.app/) for `hidutil`)
- `additional tools for xcode` [here](https://developer.apple.com/download/all/) includes
	- AU Lab (I've used this to set up an audio monitor) 
	- Link Conditioner (so you can set up a system-wide network with whatever properties you want - i.e. you can limit your network speed, add latency, etc) and more
- `plutil` is for editing property list files
- `security` for interacting with the keychain (see [[keychain command line access]])
- `defaults` for setting OS config (see [[prefsniff]])
- `afconvert` for converting audio formats
	- `afconvert music.wav -o music_160kbps_aac.m4a -b 160000 -q 127 -s 2 -f m4af -d 'aac '`
- `afinfo` for info about an audio file
- `fs_usage` -  report system calls and page faults related to filesystem activity in real-time
- `mdls` - It's ls for metadata. Scripted access to the date/time when and the latitude/longitude where a photograph was taken
	- example usage, get an application's bundle identifier:
	```
	$ mdls -name kMDItemCFBundleIdentifier -r /Applications/IINA.app
	com.colliderli.lina
	```
	- useful in concert with  [[duti]]
- `system_profiler` - command line access to system information
	- `system_profiler SPHardwareDataType` will give you a listing of your basic hardware information. Super handy, I'd never heard of this before
- `sw_vers` - print OS and hardware version
- `iperf3-darwin` – perform network throughput tests
- `lipo` - thin universal binaries to only a particular/a set of supported architectures
	- `lipo <universal exe/dylib> -thin arm64e -output <new apple silicon-only exe/dylib>`
	- neat!
- `dscl` - Directory Service command line utility (manage users and groups)
- `scutil` - Manage system configuration parameters (useful for checking current DNS configuration and checking reachability to a host).
	- `scutil --dns` will print the DNS settings of your machine
	- Here's me checking a computer on my local network:
```
$ scutil -r qfwfq.local
Reachable
```
- `sysadminctl` - doesn't have a man page, but has various user and system functionalities
	- run without arguments to get a sense of them
	- `deleteUser`, `newPassword`, `screenLock`, and more

- using `sips` and `iconutil` to generate a full iconset from a 1024x1024 png:
```
mkdir MyIcon.iconset
cp Icon1024.png MyIcon.iconset/icon_512x512@2x.png
sips -z 16 16     Icon1024.png --out MyIcon.iconset/icon_16x16.png
sips -z 32 32     Icon1024.png --out MyIcon.iconset/icon_16x16@2x.png
sips -z 32 32     Icon1024.png --out MyIcon.iconset/icon_32x32.png
sips -z 64 64     Icon1024.png --out MyIcon.iconset/icon_32x32@2x.png
sips -z 128 128   Icon1024.png --out MyIcon.iconset/icon_128x128.png
sips -z 256 256   Icon1024.png --out MyIcon.iconset/icon_128x128@2x.png
sips -z 256 256   Icon1024.png --out MyIcon.iconset/icon_256x256.png
sips -z 512 512   Icon1024.png --out MyIcon.iconset/icon_256x256@2x.png
sips -z 512 512   Icon1024.png --out MyIcon.iconset/icon_512x512.png
iconutil -c icns MyIcon.iconset
```

- I found `eslogger` via a mention on [mastodon](https://federated.saagarjha.com/objects/a6aac6ed-7a4c-4bfe-9436-24d1a2f5af1b), it's fantastically useful for monitoring events on your system. See [[debugging os x]] for more details
- `xattr` allows you to modify extended filesystem attributes
	- you can open an app that says "_app_ Is Damaged and Can’t Be Opened" with `xattr -c /Applications/app.app`
	- `-c` clears all attributes