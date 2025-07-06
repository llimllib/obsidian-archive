---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://datatracker.ietf.org/doc/html/rfc9420

A standards-track IETF proposal:

> Messaging applications are increasingly making use of end-to-end security mechanisms to ensure that messages are only accessible to the communicating endpoints, and not to any servers involved in delivering messages. Establishing keys to provide such protections is challenging for group chat settings, in which more than two clients need to agree on a key but may not be online at the same time. In this document, we specify a key establishment protocol that provides efficient asynchronous group key establishment with forward secrecy (FS) and post-compromise security (PCS) for groups in size ranging from two to thousands.

[this](https://github.com/mlswg/mls-implementations/blob/main/implementation_list.md#list-of-existing-mls-implementations) seems to be a reasonably complete list of implementations