https://sandstorm.io/

# **Sandstorm** is an open source  
platform for self-hosting web apps

> ## Self-host web-based productivity apps easily and securely.

> Sandstorm is an open source project built by a community of volunteers with the goal of making it really easy to run open source web applications.

I think it's based on making it easy to run docker-compose apps?

> **Sandstorm [takes](https://sandstorm.io/how-it-works) a wildly different approach:** It containerizes _objects_, where an object is primarily defined by _data_. We call each Sandstorm container a **“grain”**, because it is fine-grained.

> For example, when using Etherpad – a document editor app – on Sandstorm, every document lives in a separate container, isolated from the others. The front-end and database for that document live in the container. The container has a private filesystem for storage. JavaScript running in the user’s browser can talk only to the document container for which it was loaded, no others. All of this makes up a single “grain”.

huh

> Building a scalable distributed system is hard. But Sandstorm developers don’t need to do that. A Sandstorm app developer needs only write an app that runs on a single machine, since a single document is unlikely ever to need more resources than that. Sandstorm will “scale” the app by running separate grains on separate machines as needed. This also simplifies the app code, as a developer need not even write logic or storage schemas to handle more than one document.

I'm not sure how they do this for apps that weren't written specifically for sandstorm? Does it refer solely to apps that are particularly written for it?

Found via [simonw](https://twitter.com/simonw/status/1570609229580627968), who noted that somebody ported datasette. I'm intrigued, but not enough to actually look into it at the moment?

Has been around a while, from searching twitter, and I'd characterize the reaction among my peers as "interested but skeptical".