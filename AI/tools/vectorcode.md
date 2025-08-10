---
created: 2025-08-04T14:56:23.032Z
updated: 2025-08-04T14:56:23.032Z
---
https://github.com/Davidyz/VectorCode/
https://github.com/Davidyz/VectorCode/blob/main/docs/cli.md

install with `uv tool install vectorcode`

I tried to use this on my work's monorepo (on aug 4 2025), but it didn't succeed for me:

- intiialize with `vectorcode init`
	- This creates a `.vectorcode` directory, as well as adds a post-checkout hook and pre-commit hook. 
	- The pre-commit hook is just `vectorcode vectorise $diff_files`, basically; the post-checkout is similar
- vectorize your code with `vectorcode vectorise **/*.ts , with whatever extensions are relevant for your project
	- it will by default ignore `.gitignore`d files
	- It helpfully notes that its database is at `~/.local/share/vectorcode/chromadb/` (thank you for using the XDG dir)
	- mutliple-extension globs seem not to be supported; you can't do `vectorcode vectorise **/*.{ts,js}`
		- you can use [include file specs](https://github.com/Davidyz/VectorCode/blob/main/docs/cli.md#file-specs) to do a similar thing, with gitignore syntax
- Unfortunately, when I go to query my code, it fails with [this bug](https://github.com/Davidyz/VectorCode/issues/24) which is marked closed but is very much open
	- I think the author marked it closed because its root cause is [this bug](https://github.com/chroma-core/chroma/issues/3486) in chromadb
