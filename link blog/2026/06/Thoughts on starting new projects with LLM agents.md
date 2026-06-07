---
created: 2026-06-07T15:29:24.348Z
updated: 2026-06-07T15:29:24.348Z
---
https://eli.thegreenplace.net/2026/thoughts-on-starting-new-projects-with-llm-agents/

Eli shares his thoughts on starting new projects with LLMs.

Many of his preferences align with mine; especially around the importance of developing a test suite that actually works. Agents are happy to give themselves huge and useless test suites if you let them test themselves.

One thing he didn't mention is static tooling - I try to load up my LLM-using projects with every possible static tooling to improve the code the LLM writes. In Go, I use [[golangci-lint]] with extra tools enabled ([ex](https://github.com/llimllib/git-ls/blob/155578fd3bdb88bc3a8531fe138d3f1fd3c11935/.golangci.yml#L5)). In python, I use [[Ruff - linter written in rust|ruff]] and [[ty]], and in typescript I use [typescript-go](https://github.com/microsoft/typescript-go) and [biome](https://biomejs.dev/) (though [oxlint](https://oxc.rs/docs/guide/usage/linter.html) seems to be gaining popularity; I've not tried it but should).