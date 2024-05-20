---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://grayduck.mn/2023/04/17/refresh-vs-long-lived-access-tokens/

> One question which I frequently receive is:

>> _Why would you want to use long-lived refresh tokens that generate short-lived access tokens as commonly seen in OAuth 2.0, versus long-lived access tokens? Aren’t you simply replacing one long-lived token with another?_
>
>There isn’t any one huge advantage that immediately stands out in favor of refresh tokens. Instead, there are a number of incremental improvements that add up towards making it the overall superior design.

Refresh token pros:
> - _It simplifies revocation_
> - _Short-lived access tokens limit the impact of them being leaked or compromised_
> - _Refresh tokens provide incremental improvements to client security_
> - _Refresh tokens allow for flexibility in future access grants_
> - allow you to _build better heuristics around abuse detection_

cons:

> - _ncreased client complexity_
> - act as a _single point-of-failure_