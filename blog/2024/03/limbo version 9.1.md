---
updated: '2024-03-10T02:36:07Z'
created: '2024-03-10T02:36:07Z'
---
[limbo](https://github.com/llimllib/limbo) is my simple and flexible open source slackbot.

This afternoon I updated all its package dependencies, got it running on python 3.12, and updated its version to from `8.6` to `9.1`. A full changelist ([diff on github](https://github.com/llimllib/limbo/compare/master%40%7B1day%7D...master)):

- updated all dependencies
- removed a few plugins that don't work
	- `calc` plugin, which used google as a calculator but no longer worked
	- `youtube` plugin, which searched youtube. I like this plugin but it didn't work and I don't feel like maintaining it. If you like it, I'd love to have a new one!
	- side note: I wish google had a realistic API
- updated python requirement to >= 3.10
	- I didn't want to drop support for 3.9 or pypy, but updating the vcrpy test fixtures didn't work with older versions of python and I don't want to spend a huge amount of time maintaining this, so I chose ease of maintenance
- removed the ancient dockerfile
- fixed the `wiki` plugin