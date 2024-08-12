---
created: 2024-08-12T16:01:18.218Z
updated: 2024-08-12T16:01:18.218Z
---
https://supabase.com/blog/postgres-new

> Introducing [postgres.new](https://postgres.new), the in-browser Postgres sandbox with AI assistance. With postgres.new, you can instantly spin up an unlimited number of Postgres databases that run directly in your browser (and soon, deploy them to S3)...

> How is this possible? The star of the show is [PGlite](https://pglite.dev/), a WASM version of Postgres that can run directly in your browser. Our friends at [ElectricSQL](https://electric-sql.com/) released PGlite a few months ago after discovering a way to compile the real Postgres source to Web Assembly (more on this later)...

> We pair PGlite with a large language model (currently GPT-4o) and give it full reign over the database with no restricted permissions or confirmations required from the user. This is actually an important detail - and has opened new doors that other AI + Postgres tools struggle with.