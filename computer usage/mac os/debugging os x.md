In order to use `dtrace` or `dtruss` like you'd use `strace` on linux, you need to disable SIP, which is a pain. There are some tools you can use though, that work with Apple's [endpoint security framework](https://developer.apple.com/documentation/endpointsecurity):
	- [here's a video from WWDC](https://developer.apple.com/videos/play/wwdc2022/110345/) about the endpoint security framework

- command line
	- `eslogger`, at `/usr/bin/eslogger`
		- list event types with `eslogger --list-events`
		- monitor the events you're interested in with `sudo eslogger [event types...]`
		- For example, `eslogger stat write unlink create` will show you file events in a jsonl format
		- the `jsonl` format also means you can use `jq` to process the events. Here's a command that will list just the executables that get `exec`ed on your system:
			- `sudo eslogger exec | jq -r '.event.exec.target.executable.path'`
	- [File Monitor](https://objective-see.org/products/utilities.html#FileMonitor) and [ProcessMonitor](https://objective-see.org/products/utilities.html#ProcessMonitor)
		- available via homebrew: `brew install filemonitor processmonitor`
		- example of usage:
		```
		$ sudo /Applications/FileMonitor.app/Contents/MacOS/FileMonitor -filter python
		{"event":"ES_EVENT_TYPE_NOTIFY_OPEN","timestamp":"2023-08-04 18:23:29 +0000","file":{"destination":"/Users/llimllib/.local/share/asdf/shims/python","process":{"pid":57014,"name":"bash","path":"/opt/homebrew/Cellar/bash/5.2.15/bin/bash","uid":501,"architecture":"Apple Silicon","arguments":[],"ppid":55569,"rpid":55327,"ancestors":[55327,1],"signing info (reported)":{"csFlags":570556931,"platformBinary":0,"signingID":"bash","teamID":"","cdHash":"A93C88D2F2D788FA7490533631214F21D6ED7BD1"},"signing info (computed)":{"signatureStatus":0,"signatureSigner":"AdHoc","signatureID":"bash"}}}}
		{"event":"ES_EVENT_TYPE_NOTIFY_CLOSE","timestamp":"2023-08-04 18:23:29 +0000","file":{"destination":"/Users/llimllib/.local/share/asdf/shims/python","process":{"pid":57014,"name":"bash","path":"/opt/homebrew/Cellar/bash/5.2.15/bin/bash","uid":501,"architecture":"Apple Silicon","arguments":[],"ppid":55569,"rpid":55327,"ancestors":[55327,1],"signing info (reported)":{"csFlags":570556931,"platformBinary":0,"signingID":"bash","teamID":"","cdHash":"A93C88D2F2D788FA7490533631214F21D6ED7BD1"},"signing info (computed)":{"signatureStatus":0,"signatureSigner":"AdHoc","signatureID":"bash"}}}}
		```
- Application UIs
	- [Crescendo](https://github.com/SuprHackerSteve/Crescendo) is OSS
		- `brew install crescendo`
	- [Red Canary Mac Monitor](https://redcanary.com/mac-threat-analysis-tool/)
		- `brew install red-canary-mac-monitor`

All of them use the same framework, so they all seem to give the same results