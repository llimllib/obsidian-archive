---
created: 2025-12-31T14:54:50.522Z
updated: 2025-12-31T14:54:50.522Z
---
- [coding](#coding)
- [tools](#tools)
- [travel](#travel)

## coding

I didn't do that much work in the open this year, unfortunately. I made a few small tools and polished my workflow scripts quite a bit though:

### review

I use my [review script](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/review) to get feedback from an LLM on a pull request before I submit it, or to review other people's PRs. I like this a lot more than tools that annotate a PR in github, because it lets me read it locally and privately, and decide for myself which of its suggestions are valuable.

As I [wrote when I released the tool](https://notes.billmill.org/blog/2025/07/An_AI_tool_I_find_useful.html), I find that _most_ of its suggestions are not useful, but having a list of suggestions to evaluate has proved a very valuable resource for me and has prevented me from making quite a few obvious errors.

### worktree

My [worktree script](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/worktree) helps me [use git worktrees](https://notes.billmill.org/blog/2024/03/How_I_use_git_worktrees.html) in a large node.js monorepo at work without so much pain. This year I:

- added submodule support
- added support for github fork notation (`user/repository`)
- added the ability to store its config in git global config

I did play with [`jj` a bit this year](https://notes.billmill.org/computer_usage/jujutsu/notes_on_giving_jj_a_try.html), but I'm so used to git that it's not a pain point for me and it seems like a waste of time, though I remain interested in it.

### time

My favorite [tiny script](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/%2Ctime) of the year is my `time` script, which I wrote because I often have to compare times in different timezones with different time formats. For example, sometimes I'm reading timestamps from a log message in milliseconds since the epoch, and I need to know when that was both in my local time and in UTC.

It has two functions:
- when called without arguments, prints out the current time in a variety of formats, useful for comparing time between timezones or formats:

```console
$ ,time
ts seconds: 1767193930.0
ts ms:      1767193930000
Local:      2025-12-31 10:12:10 EST
UTC:        2025-12-31 15:12:10 UTC
```

- if passed an argument, will do its best to parse the time and display it in those same formats:

```console
$ ,time 1756082819
ts seconds: 1756082819.0
ts ms:      1756082819000
Local:      2025-08-24 20:46:59 EDT
UTC:        2025-08-25 00:46:59 UTC

$ ,time Dec 31 2024
ts seconds: 1735621200.0
ts ms:      1735621200000
Local:      2024-12-31 00:00:00 EST
UTC:        2024-12-31 05:00:00 UTC
```

### gp

I have the rights to push to the main branch of a bunch of git repositories, and I found myself occasionally pushing directly to main by accident instead of creating a branch.

To solve that problem, I replaced my `git push` alias with [a script](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/gp) that checks if I'm pushing to a main branch by accident, and displays a message to the console with the ability to do the push if it was indeed intentional.

## tools

I still spend most of my life in neovim in the terminal, and have no desire to change either of those.

I'd like to switch to [ghostty](https://ghostty.org), but it doesn't support opening hyperlinks in terminal applications ([github discussion](https://github.com/ghostty-org/ghostty/discussions/9546)). I find this workflow incredibly useful and don't want to live without it, so I'm still using [kitty](https://sw.kovidgoyal.net/kitty/).

I've been using Obsidian to make this website, and remain very happy with it. 

I've updated the [script that builds the website](https://github.com/llimllib/obsidian_notes/blob/main/run.py) in minor ways throughout the year. It's slow and I dislike the [markdown library it uses](https://pypi.org/project/markdown-it-py/), but it also gets the job done and I don't have to think about it.

> [!tip] I added hacky callout support
> But it was hacky and painful to do, so it goes

I switched from Firefox to [Orion](https://orionbrowser.com) browser, which is working well enough though it definitely has some bugs. I tend to switch browsers every six months as I accumulate dissatisfactions with all of them.

### games

For a long time, I've vaguely wanted to play games that are Windows-only, but I also refuse to install Windows and I don't have a Linux gaming computer set up. A couple weeks ago, I finally bit the bullet and purchased [CrossOver](https://www.codeweavers.com) and have started playing a few games that are Windows-only.

Some games I or my kids enjoyed this year:

- We all enjoyed [N++](https://www.metanetsoftware.com/games/nplusplus), a platformer stripped down to the absolute basics. I remember playing [n](https://www.metanetsoftware.com/games/n) as a flash game so many years ago, and its older sibling is still a blast.
- I enjoyed playing [Animal Well](https://www.animalwell.net)
- Because [Silksong](https://hollowknightsilksong.com) came out this year, I went back and tried to finish [Hollow Knight](https://www.hollowknight.com). I managed to get to the last boss, but couldn't beat him, and didn't end up buying Siksong. Maybe next year
- My older son really enjoyed [Ball x Pit](https://www.ballxpit.com)
- My younger son got old enough to play [Tears of the Kingdom](https://www.nintendo.com/us/store/products/the-legend-of-zelda-tears-of-the-kingdom-switch/) for himself, and enjoys coming up with silly weapon combinations more than actually playing the story, which is fun
- We had fun playing some [FTL](https://subsetgames.com/ftl.html) runs together
- We all had fun with [Dead Cells](https://deadcells.com)

## travel

Working for a [distributed company](https://readme.com) means traveling for meetups, and we had them in particularly fun locations this year. I was fortunate to travel to Colorado, Montana, and Mexico for work this year.

![[0698C573-F6A1-4854-9697-CB3AC2CCB32B_1_105_c.jpeg]]

![[58CEAC05-38D6-4FC5-B259-72794BB0932D_1_105_c.jpeg]]

![[E9BBB1DE-DF26-4BE3-9B67-DC56400E5492_1_105_c.jpeg]]

My family and I spent two weeks in Lecco, Italy, which was gorgeous. I'd never been to Italy before and it was great

![[6ED76249-39D2-496A-BBD1-5551659B3E9B_1_105_c.jpeg]]