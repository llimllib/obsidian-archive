https://www.forrestthewoods.com/blog/using-zig-to-commit-toolchains-to-vcs/

The author demonstrates how they created a C++ "hello world" application that contains everything necessary to compile and build itself on all supported platforms.

> I strongly believe that all dependencies - including compiler toolchains - belong in version control. It's radically more usable, reliable, reproducible, and sustainable. A new and improved VCS tool can make this space and bandwidth efficient.

> My sample project demonstrates that vendoring toolchains absolutely works. It can be done. Even on Linux.

To do so, they end up with a 1.23gb repository, so I think it's safe to consign this to the realm of the not currently practical. It is an appealing idea though, and it's worth reading the challenges involved in making it work.