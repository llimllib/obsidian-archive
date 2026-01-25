---
created: 2026-01-15T21:24:33.835Z
updated: 2026-01-15T21:24:33.835Z
---
https://github.com/llimllib/aver

While I was working on [[mdriver]], I got annoyed that the LLM was giving me old github actions versions, something I've seen it consistently do.

So I created `aver`, which checks for all github actions versions in a project and prints a list if any are out of date. If everything is up to date, it returns a zero status code; otherwise it returns a nonzero status code.

One thing I wasn't sure about with it was what to do with pinned actions references - if you have an opinion, file an issue or let me know!

It's easy to integrate `aver` with LLMs as either a skill, or just putting a reference to it in `CLAUDE.md`, so that they will stop giving you out of date GitHub actions workflow versions.

I got the idea from [[actions-latest]], but I wanted to have that information for any action, not just the official github actions.

Check it out, and let me know! I think there's a lot of people out there annoyed by this.