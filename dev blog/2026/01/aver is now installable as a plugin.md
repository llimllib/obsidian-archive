---
created: 2026-01-29T20:28:53.794Z
updated: 2026-01-29T20:28:53.794Z
---
I updated [[aver]] so that it can be installed via the claude [plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces), so you can install it in claude code with:

```
/plugin marketplace add llimllib/aver
/plugin install github-actions-version-check@aver
```

`aver` is a GitHub **A**ctions **ver**sion checker. Scans your GitHub actions workflow files and reports outdated versions. Adding the skill should prevent claude from using old versions of plugins