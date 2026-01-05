---
created: 2026-01-05T14:10:47.877Z
updated: 2026-01-05T14:10:47.877Z
---
https://github.com/llimllib/mdstream

I've wanted a markdown parser like [[glow]] for a while, with the one major change that it streams its output to the console instead of buffering the whole file for display.

The idea is that I can pipe llm output to it and have it display immediately, instead of waiting to buffer the whole thing.

Currently, I use [[bat]] for the job with this zsh alias:

```
# create a function that pipes llm output through bat to highlight markdown
llm() {
  command llm "$@" | bat --paging=never --style=plain --language=markdown
}
```

But it doesn't do as nice a job of rendering the output as `glow` does. So I want something that works as well as bat and looks as nice as glow, but also I don't want to do the work!

So I signed up for a claude pro account and tried to generate the whole thing in rust, which I can read well enough but don't really know how to write.

The result so far isn't bad, but I'm out of usage until next week already:

![[Screen Recording 2026-01-05 at 9.18.52 AM.mov]]

The state of things is definitely improving! Claude generated the tool without me touching a line of code.

But it's still very expensive. I'm on a $20/month plan and I used up a week's worth in a night and a morning of hacking, about 3 hours total of machine time.

The TODO list for the app is:

- fuller markdown support:
	- strikethrough
	- tables
	- horizontal rules
- a github action to build a release for a selection of platforms