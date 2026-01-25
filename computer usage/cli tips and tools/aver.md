---
created: 2026-01-17T01:38:45.658Z
updated: 2026-01-17T01:38:45.658Z
---
> A GitHub **A**ctions **ver**sion checker. Scans your GitHub actions workflow files and reports outdated versions.

`aver` checks your github actions files for any outdated actions, and returns a non-zero status code if it finds any. The output currently looks like:

```
$ aver
Outdated actions:
File                            Action                   Current  Latest
------------------------------  -----------------------  -------  ------
.github/workflows/fixture.yaml  tailscale/github-action  v3       v4.1.1

SHA-pinned actions behind default branch:
File                            Action            Current SHA  Latest SHA  Branch  Behind
------------------------------  ----------------  -----------  ----------  ------  ------
.github/workflows/fixture.yaml  actions/checkout  d632683      0c366fd     main    26    
.github/workflows/fixture.yaml  actions/setup-go  3d65fa5      7a3fe6c     main    54    
```

The idea here is that you can help your LLM to create GitHub actions that don't use outdated version of actions. There's [a skill](https://github.com/llimllib/aver/blob/main/skill/github-actions-version-check/SKILL.md) available in the repository that you can use with [[claude code]] or [[pi]].

You can install it with homebrew: `brew install limllib/tap/aver` or with go: `go install github.com/llimllib/aver/cmd/aver@latest`