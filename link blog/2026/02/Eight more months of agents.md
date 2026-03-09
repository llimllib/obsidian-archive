---
created: 2026-02-23T12:18:26.615Z
updated: 2026-02-23T12:18:26.615Z
---
> Most software is the wrong shape now. Most of the ways we try to solve problems are the wrong shape.
> 
> To give you an example, consider Stripe Sigma. This product is a nice new SQL query system for your Stripe DB. It has a little LLM built into it to help you write queries. The LLM is not very good. I want Claude Code or Codex writing my queries. But Stripe launched a fancy Sigma UI with an integrated helper before their API. There is a private alpha for the SQL REST endpoint that I do not have access to yet. So instead I had my agent do ETL-from-scratch: it used the standard Stripe APIs to query everything about my account, build a local SQLite DB, and now my agent queries against that far better than Sigma can.
> 
> I implemented that entire Stripe product (as it relates to me) by typing three sentences. It solves my problem better than their product.

- [David Crawshaw](https://crawshaw.io/blog/eight-more-months-of-agents)