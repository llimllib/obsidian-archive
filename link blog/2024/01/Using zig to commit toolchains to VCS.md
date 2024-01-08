https://www.forrestthewoods.com/blog/using-zig-to-commit-toolchains-to-vcs/

The author demonstrates how they created a C++ "hello world" application that contains everything necessary to compile and build itself on all supported platforms.

> I strongly believe that all dependencies - including compiler toolchains - belong in version control. It's radically more usable, reliable, reproducible, and sustainable. A new and improved VCS tool can make this space and bandwidth efficient.

> My sample project demonstrates that vendoring toolchains absolutely works. It can be done. Even on Linux.

To do so, they end up with a 1.23gb repository, so I think it's safe to consign this to the realm of the not currently practical. It is an appealing idea though, and it's worth reading the challenges involved in making it work.

The author also has [this article](https://www.forrestthewoods.com/blog/dependencies-belong-in-version-control/) describing why they think VCSes should support this sort of repository, and how it can be made practical if they do.

> I believe that all project dependencies belong in version control. Source code, binary assets, third-party libraries, and even compiler toolchains. Everything.

> A user should be able to perform a clean OS install, download a zip of master, disconnect from the internet, and build. The build process shouldn't require installing any extra tools or content. If it's something the build needs then it belongs in version control.

---

> In theory Git could be updated to more properly support large projects. I believe Git should be shallow and partial by default. Almost all software projects are defacto centralized. Needing full history isn't the default, it's an edge case. Users should opt-in to full history only if they need it.

> ...My snarky opinion is that Docker and friends primarily exist because modern build systems are so god damned fragile that the only way to reliably build and deploy is to create a full OS image. This is insanity!

> Containers shouldn't be required simply to build and run projects. It's embarassing that's the world we live in.