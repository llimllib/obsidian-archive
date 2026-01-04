---
created: 2024-07-31T12:49:34.824Z
updated: 2026-01-04T21:26:52.103Z
---
https://github.com/olimorris/codecompanion.nvim

Been using this for a while now and really like it.

---

setting up claude code ([docs](https://codecompanion.olimorris.dev/configuration/adapters-acp#setup-claude-code)) and using the apple keyring for the API key:

- install claude ACP

```shell
npm install -g @zed-industries/claude-code-acp
```

- get a claude token

```shell
claude setup-token
```

- save the token to the keyring:
```console
security add-generic-password -s 'anthropic-claude' -w 'sk-ant-<token-here>'
```

- configure codecompanion to use it:
```lua
acp = {
	claude_code = function()
		return require("codecompanion.adapters").extend("claude_code", {
			env = {
				CLAUDE_CODE_OAUTH_TOKEN = "cmd:security find-generic-password -ws 'anthropic-claude' | tr -d '\n'",
			},
		})
	end,
},
```

Then update your config to use the `claude_code` adapter where you want to use it.

[Here's the change I made](https://github.com/llimllib/personal_code/commit/6dea04e21f573837f7cc0ace47839fe9078b5eb9) to my dotfiles to implement this