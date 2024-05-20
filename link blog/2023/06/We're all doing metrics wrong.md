---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://matduggan.com/were-all-doing-metrics-wrong/

> Logs make sense as a concept but they don't work as an actual tool unless you are willing to basically commit real engineering time every cycle to keeping the logging functional OR you are willing to throw a lot of cash at a provider. On top of that, soon you'll have people writing log parsers to alert on certain situations happening which _seems fine_, but then the logs become even MORE critical and now you need to enforce logging structure standards or convert old log formats to the new format.

...

> When you have a log that must be stored for compliance or legal reasons, don't stick it into the same system you use to store every 200 - OK line. Write it to a database (ideally) or an object store outside of the logging pipeline.

oh man I love this idea for adaptive sampling:

> - Sampled logs being more of a thing. My dream would be to tie them to deployments so I crank the retention to 100% before I deploy, as I deploy and then for some period of time after I deploy. The collector makes an API call to see what is the normal failure rate for this application (how many 2xx, 4xx, 5xx) and then if the application sticks with that breakdown increase the sampling.
> 