https://github.com/simonw/llm
https://llm.datasette.io/en/stable/index.html

Simonw's [llm tool](https://llm.datasette.io/en/stable/index.html) for the command line.

I wrote my own [gpt wrapper](http://github.com/llimllib/gpt) that I use for gpt, but I wanted to try out anthropic and I'm way too lazy to update it, so I thought I'd give Simon's tool a shot.

Setup:

- `brew install llm`
- `llm install llm-claude-3`
	- Installs the [llm-claude-3 plugin](https://github.com/simonw/llm-claude-3)
	- I wish the CLI could list/search plugins
	- I found the plugin name [here](https://llm.datasette.io/en/stable/plugins/directory.html)
- `llm keys set claude` and paste the claude API key from [here](https://console.anthropic.com/settings/keys)
	- I didn't read the plugin readme, and added a key with the wrong name, but unfortunately there's no `llm keys remove` command
- `llm models default claude-3-sonnet`

Now `claude-3-sonnet` (the middle tier claude 3 model, it goes `haiku` < `sonnet` < `opus`) is set as the default model and you can chat with `llm 'prompt goes here'`.

- `-c` to continue a conversation; my tool has the opposite default, but I think this makes more sense.
- `-s` to give a system prompt
- `llm chat` to have an interactive chat, `llm chat -c` to continue from the previous prompt
