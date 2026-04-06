---
created: 2026-04-06T12:59:38.724Z
updated: 2026-04-06T12:59:38.724Z
---
https://agent-safehouse.dev/
https://agent-safehouse.dev/docs/overview.html

via [news.yc](https://news.ycombinator.com/item?id=47301085)

> Agent Safehouse sandboxes LLM coding agents on macOS so they can only access paths they need.

> It uses macOS sandbox-exec with composable policy profiles. The default posture is strict: start from deny-all, then allow specific system/runtime/toolchain paths plus explicitly granted project paths.
> Why
> 
> LLM coding agents run shell commands with your user privileges. A prompt injection, confused deputy flow, or a bad command can otherwise touch SSH keys, cloud credentials, unrelated repos, and personal files.
> 
> Safehouse reduces that blast radius without requiring major workflow changes.
> Guiding Philosophy
> 
> Agent productivity is prioritized over paranoid lockdown. The goal is practical damage reduction and stronger defaults, not perfect isolation against a determined attacker.
> 
> Each policy rule should answer one question:
> 
>     Does the agent need this to do its job?