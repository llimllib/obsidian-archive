---
created: 2026-01-13T14:49:10.147Z
updated: 2026-01-13T14:49:10.147Z
---
https://shittycodingagent.ai (lol, aka https://buildwithpi.ai)
https://github.com/badlogic/pi-mono/
https://www.npmjs.com/package/@mariozechner/pi-coding-agent

pi is a coding agent CLI competitive with [[claude code]], distinguished by the things it doesn't have. The author wrote a [nice post](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/) in which they described why they built it as they did.

> Exactly controlling what goes into the model's context yields better outputs, especially when it's writing code. Existing harnesses make this extremely hard or impossible by injecting stuff behind your back that isn't even surfaced in the UI

> Speaking of surfacing things, I want to inspect every aspect of my interactions with the model. Basically no harness allows that. I also want a cleanly documented session format I can post-process automatically, and a simple way to build alternative UIs on top of the agent core.

---

## Installation notes

The recommended install command, `npm install -g @mariozechner/pi-coding-agent` failed for me when trying to install `sharp`; I filed [an issue here](https://github.com/badlogic/pi-mono/issues/696) but the upshot was that I needed to run `$ npm install -g node-addon-api node-gyp @mariozechner/pi-coding-agent` so that `sharp` could build itself.

[this issue](https://github.com/badlogic/pi-mono/issues/534) suggests that you can use `PI_CONFIG_DIR` to tell `pi` not to use `~/.pi` for config

annoyingly, I can't tell it to pull my anthropic keys from [[keychain command line access|keychain]], it requires a config file or an environment variable, both of which are quite a bit less secure. I [filed an issue here](https://github.com/badlogic/pi-mono/issues/697)

I logged in with `/login` and was able to set it to use my claude code subscription, which it saved to `~/.pi` even though I have set `PI_CONFIG_DIR` to `~/.config/pi`.

It actually seems as though `PI_CONFIG_DIR` is only supported by the `pods` module, not the coding agent, which is disappointing.