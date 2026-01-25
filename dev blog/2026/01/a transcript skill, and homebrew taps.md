---
created: 2026-01-17T01:38:05.887Z
updated: 2026-01-17T01:38:05.887Z
---
## a transcript skill

I had been telling [[claude code]], and then [[pi]] to generate a transcript and add it to the PR, and both of them had been generating the export and attaching it as a gist link.

I don't like the idea of relying on gist in the long term though, so I updated each repository with [a skill](https://github.com/llimllib/mdriver/blob/main/.pi/skills/pr-transcript/SKILL.md) that teaches [[pi]] how to make an HTML transcript and put it in the [transcripts directory](https://github.com/llimllib/mdriver/tree/main/transcripts) of the project.

Unfortunately, github doesn't allow for the preview of HTML pages, so I think my next step may be to whip up a documentation site for each that includes the transcripts.
## taps

Today I added homebrew taps for [[aver]] and [[mdriver]], which you can now install as `brew install llimllib/tap/aver` and `brew install llimllib/tap/mdriver`, respectively.

[[goreleaser]] made this a breeze, and I used it for both projects. 

The LLM also decided to use [cargo-zigbuild](https://github.com/rust-cross/cargo-zigbuild) for cross-compiling `mdriver`, it looks like a neat project and worked without any hassle.
### aver

- I added hyperlinks to the `aver` output, so you can click on an action name to go directly to that action's repository on GitHub, on a version to go to the release notes for that version, or on a sha to go directly to that sha
- I added a progress spinner so you know it's doing something; you can turn it off with `--quiet`
![[Pasted image 20260116205001.png]]

### mdriver

- I added task list parsing - filled in tasks were being treated as reference links, but now will be displayed nicely

![[Pasted image 20260116204927.png]]