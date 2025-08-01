---
updated: '2023-11-09T14:54:44Z'
created: '2023-11-09T14:54:44Z'
---
https://automerge.org/blog/2023/11/06/automerge-repo/

> A challenge in local-first software is how to merge edits that were made independently on different devices, and [CRDTs](https://crdt.tech/) were developed to solve this problem. Automerge is a fairly mature CRDT implementation. In fact, we wrote this blog post using it! The API is quite low-level though, and Automerge-Core has no opinion about how networking or storage should be done. Often, the first thing developers ask after discovering Automerge was how to connect it into an actual application.

> Our new library, `automerge-repo`, extends the collaboration engine of Automerge-Core with networking and storage adapters, and provides integrations with React and other UI frameworks. You can get to building your app straight away by taking advantage of default implementations that solve common problems such as how to send binary data over a WebSocket, how often to send synchronization messages, what network format to use, or how to store data in places like the browser's IndexedDB or on the filesystem.