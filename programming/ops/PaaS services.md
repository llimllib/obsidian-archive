---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Heroku is dead(ish), who's competing in the forever-next-heroku market?

# Render

https://render.com/

> Render is a unified cloud to build and run all your apps and websites with free TLS certificates, a global CDN, DDoS protection, private networks, and auto deploys from Git.

Pretty explicitly a continuation of what Heroku was doing

# fly.io

https://fly.io/

> Run your full stack apps (and databases!) all over the world. No ops required.

Focuses on running containerized apps anywhere you want to run them. They have database support but it's not exactly clear to me how it works, despite having read voluminous blog entries with details on how it does.

# Crunchy Data

I'm going to include services that only take on part of the Heroku stack in this list; I'm not sure if disaggregated PaaS makes sense to me but it might.

https://www.crunchydata.com/

Crunchy data runs a postgres database for you, if I understand correctly - I'm not sure how I would integrate it into another service, but that's probably because I've done literally zero research.

> No matter the industry or size of your company, Crunchy Data is the trusted partner companies rely upon for their Postgres needs. From startups to Fortune 500, healthcare, software development, autonomous vehicles, government agencies, financial services to decentralized finance companies.

# supabase

https://supabase.com/

> Create a backend in less than 2 minutes. Start your project with a Postgres Database, Authentication, instant APIs, Realtime subscriptions and Storage.

Focuses on really pushing postgres into the app space.

[[Supabase]]

# planetscale

https://planetscale.com/

> The MySQL-compatible serverless database platform.

[[Vitess]]