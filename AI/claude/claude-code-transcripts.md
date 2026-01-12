---
created: 2026-01-12T18:43:19.218Z
updated: 2026-01-12T18:43:19.218Z
---
https://github.com/simonw/claude-code-transcripts
https://simonwillison.net/2025/Dec/25/claude-code-transcripts/#atom-everything

> I’ve released [claude-code-transcripts](https://github.com/simonw/claude-code-transcripts), a new Python CLI tool for converting [Claude Code](https://claude.ai/code) transcripts to detailed HTML pages that provide a better interface for understanding what Claude Code has done than even Claude Code itself. The resulting transcripts are also designed to be shared, using any static HTML hosting or even via GitHub Gists.
> 
> Here’s the quick start, with no installation required if you already have [uv](https://docs.astral.sh/uv/):

```console
$ uvx claude-code-transcripts
```

I've started figuring out that I want to include my chat transcript along with the PRs that code generates, but I haven't yet settled on a satisfactory design for how to do so.