https://www.sigbus.info/worse-is-better

A nice essay about how converting lld (the llvm linker) from a nifty abstract design to a simpler concrete one made it faster and less complex.

> lld v2 consists of virtually three different linkers for Windows, macOS and Unix. They share the same design but do not share code. Naturally, we sometimes had to write very similar code for each target. This may seem like an amateur-level programming mistake, but in reality, it's much easier to write straightforward code for each target than writing unified one that covers all the details and corner cases of all supported targets simultaneously.