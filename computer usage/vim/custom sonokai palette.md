To get my own color scheme, I had been using a [fork of](https://github.com/llimllib/lilium) [sonokai](https://github.com/sainnhe/sonokai) that I had created. 

I don't remember why I created it instead of using a custom palette with sonokai, but recently my color scheme (which I had never maintained) broke when viewing markdown files, so this morning I figured out how to switch back to sonokai and just use my custom palette.

It was very easy:

```lua
vim.g.sonokai_colors_override = {
	black = { "#181a1c", "232" },
	bg_dim = { "#24272e", "232" },
	bg0 = { "#252A39", "235" },
	bg1 = { "#2a3041", "236" },
	bg2 = { "#2f3548", "236" },
	bg3 = { "#343b50", "237" },
	bg4 = { "#394158", "237" },
	bg_red = { "#ff6d7e", "203" },
	diff_red = { "#55393d", "52" },
	bg_green = { "#a5e179", "107" },
	diff_green = { "#394634", "22" },
	bg_blue = { "#7ad5f1", "110" },
	diff_blue = { "#354157", "17" },
	diff_yellow = { "#4e432f", "54" },
	fg = { "#e1e3e4", "250" },
	red = { "#F47648", "203" },
	orange = { "#8ED0B2", "215" },
	yellow = { "#8ED0B2", "179" },
	green = { "#40BA93", "107" },
	blue = { "#73D0FF", "110" },
	purple = { "#fca07f", "176" },
	grey = { "#828a9a", "246" },
	grey_dim = { "#5a6477", "240" },
	none = { "NONE", "NONE" },
}
vim.cmd("colorscheme sonokai")
```

[here it is in context of my config](https://github.com/llimllib/personal_code/blob/68106a99/homedir/.config/nvim/lua/colorscheme.lua#L1-L27); I have archived my fork of sonokai because there's no longer any reason for it to exist.

Some screenshots of my custom theme:

![[Pasted image 20240302095147.png]]

![[Pasted image 20240302095255.png]]

![[Pasted image 20240302095354.png]]