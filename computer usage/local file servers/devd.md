---
updated: '2024-03-11T18:53:05Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/cortesi/devd

no longer maintained, but still works and has been a favorite of mine for a long time. May switch to [[duf]] if it gets stale for some reason.

---

Open a devd server on port 1234 with a self-signed https cert, and proxy all requests on plain http to 1235:

```
 devd -s -p 1234 http://localhost:1235
 ```