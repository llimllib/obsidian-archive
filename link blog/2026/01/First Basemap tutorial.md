---
created: 2026-01-05T21:04:05.790Z
updated: 2026-01-05T21:04:05.790Z
---
https://palewi.re/docs/first-basemap/

A nice tutorial that walks you through using [[planetiler]] and [[PMTiles]] to create a custom basemap, and then [[MapLibre]] to display it.

It uses github actions to spin up a large EC2 instance for a few hours to create the map files, which it stores on s3. I had a couple of thoughts while reading it:
- I wish they'd used OIDC instead of access tokens, I could help spread knowledge of that flow
- It would be cool to modify the tutorial to do the work on a computer at my house via tailscale, like I do with [[NBA data]]