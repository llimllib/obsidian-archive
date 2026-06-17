---
created: 2026-06-17T12:03:35.720Z
updated: 2026-06-17T12:03:35.720Z
---
https://github.com/losfair/zeroserve

- introduction post: https://su3.io/posts/introducing-zeroserve
- Caddy compatibility layer: https://su3.io/posts/zeroserve-caddy-compat

A clever idea to run a web server as a set of eBPF scripts

> Scripts are compiled to eBPF and JIT-executed per request inside a memory- and time-bounded sandbox. The helper API covers request/response inspection and mutation, response templating, logging and time, crypto and encoding (SHA-256, HMAC, base64, hex, random), AWS SigV4 signing, rate limiting, reverse proxy, OAuth2/OIDC login with sealed cookies, and strongSwan VICI lookups.