https://github.com/TypeStrong/ts-node

> ts-node is a TypeScript execution engine and REPL for Node.js.

> It JIT transforms TypeScript into JavaScript, enabling you to directly execute TypeScript on Node.js without precompiling. This is accomplished by hooking node's module loading APIs, enabling it to be used seamlessly alongside other Node.js tools and libraries.

What my project at work currently uses. Compare to [[tsx - run typescript code]], which looks interesting.

Seems to do the job fine, but I've never trusted it to run in production; we use it only for running small things locally.