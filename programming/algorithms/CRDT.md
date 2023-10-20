Yjs and Automerge are the two implementations I've heard of people actually using:

https://github.com/yjs/yjs

> Yjs is a [CRDT implementation](https://github.com/yjs/yjs#Yjs-CRDT-Algorithm) that exposes its internal data structure as _shared types_. Shared types are common data types like `Map` or `Array` with superpowers: changes are automatically distributed to other peers and merged without merge conflicts.

https://github.com/automerge/automerge

> Automerge is a library of data structures for building collaborative applications in JavaScript.

I enjoyed this talk: https://www.youtube.com/watch?v=x7drE24geUw

Why CRDTs didn't work for Xi: https://github.com/xi-editor/xi-editor/issues/1187#issuecomment-491473599

Why Marijn Haverbeke chose OT rather than CRDT: https://marijnhaverbeke.nl/blog/collaborative-editing-cm.html