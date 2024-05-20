---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://redcanary.com/blog/mac-monitor/

> [Red Canary Mac Monitor](https://redcanary.com/mac-threat-analysis-tool) is a feature-rich dynamic analysis tool for macOS that leverages our extensive understanding of the platform and Apple’s latest APIs to collect and present relevant security events. Mac Monitor is practically the macOS version of the [Microsoft Sysinternals](https://learn.microsoft.com/en-us/sysinternals/) tool [Procmon](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon). Mac Monitor collects a wide variety of [telemetry classes](https://developer.apple.com/documentation/endpointsecurity/3228936-es_events_t), including processes, interprocess, files, file metadata, logins, XProtect detections, and more—enabling defenders to quickly and effectively analyze enriched, high-fidelity macOS security events in a native, modern, and customizable user interface.

1. `brew install --cask red-canary-mac-monitor`
2. start `Red Canary Mac Monitor` 
3. it will ask for permission to run a kernel module, grant that permission
4. quit and restart the app
5. hit "start", then you are watching the kernel events occuring on your mac in real(-ish) time
6. very neat!
![[Pasted image 20230502150350.png]]

via [news.yc](https://news.ycombinator.com/item?id=35787114)