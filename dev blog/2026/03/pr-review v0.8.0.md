---
created: 2026-04-06T12:59:38.772Z
updated: 2026-04-06T12:59:38.772Z
---
I was inspired by claude's PR [review agent announcement](https://claude.com/blog/code-review) to do some work on release version **0.8.0** of [[pr-review]] today:

- Much nicer output that shows you what it's doing  
- If you pass `-v`, the agents log all activity  
- A `--html <session_id>` flag to output an HTML page with the results of each sub-agent's review  
- Includes `AGENTS.md` context for the review agents by default, you can disable it with `--no-context`

Get it at https://github.com/llimllib/pr-review or with `brew install llimllib/tap/pr-review`

Here's what the new verbose output looks like:

![[Pasted image 20260310135735.png]]