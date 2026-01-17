---
created: 2026-01-17T01:50:47.580Z
updated: 2026-01-17T01:50:47.580Z
---
https://goreleaser.com/
https://github.com/goreleaser/goreleaser

> Release engineering, simplified.

I've used this in a couple projects to handle:

- building a binary
- making a github release
- creating a homebrew tap

And it makes my life easier.

The name is a bit misleading, it can build releases for go, rust, zig, bun, deno and python projects.

- in [[mdriver]], which is a rust project, [here's the goreleaser config](https://github.com/llimllib/mdriver/blob/main/.goreleaser.yaml) and [here's the release action](https://github.com/llimllib/mdriver/blob/main/.github/workflows/release.yml)
	- [here's an example release it built](https://github.com/llimllib/mdriver/releases/tag/v0.10.1)
- In [[aver]], a go project, it's substantially the same. [goreleaser config](https://github.com/llimllib/aver/blob/main/.goreleaser.yaml) and [release config](https://github.com/llimllib/aver/blob/main/.github/workflows/release.yml)