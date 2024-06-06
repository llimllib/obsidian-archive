---
created: 2024-06-06T14:04:23.197Z
updated: 2024-06-06T14:04:23.197Z
---
One of the first things I setup on my computer; I use it for:
- filename completion
	- type `cat src/**<tab>`, and a list of files pops up where I can start typing and get fuzzy completion
	- [config here](https://github.com/llimllib/personal_code/blob/07025b5e005f0211272d306c7bc758576822c533/homedir/.zshrc#L321-L356)
- telescope
	- my favorite [vim extension](https://github.com/nvim-telescope/telescope.nvim), which I use constantly, uses fzf to filter file names
	- [config here](https://github.com/llimllib/personal_code/blob/07025b5e005f0211272d306c7bc758576822c533/homedir/.config/nvim/lua/telescope-cfg.lua)
- `,ff`: my personal file finder script, which is an [[fd]] command piped to fzf, which shows a preview of a file and pops it open in vim if you select it
	- [source](https://github.com/llimllib/personal_code/blob/07025b5e005f0211272d306c7bc758576822c533/homedir/.local/bin/%2Cff)
	- screenshot:
![[Pasted image 20240606101100.png]]
- `,fg`: a similar script, but greps inside the files rather than searching the file names and shows the match in context
	- [source](https://github.com/llimllib/personal_code/blob/07025b5e005f0211272d306c7bc758576822c533/homedir/.local/bin/%2Cfg)
	- screenshot (here I've searched for `render`, and it shows the selected match in context):
![[Pasted image 20240606101430.png]]

The fzf [docs have a neat tip](https://junegunn.github.io/fzf/tips/browsing-log-streams/) about using `fzf` to browse log files from a server interactively