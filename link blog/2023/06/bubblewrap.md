---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/containers/bubblewrap

> The goal of bubblewrap is to run an application in a sandbox, where it has restricted access to parts of the operating system or user data such as the home directory.

...

> bubblewrap is a tool for constructing sandbox environments. bubblewrap is not a complete, ready-made sandbox with a specific security policy.

> Some of bubblewrap's use-cases want a security boundary between the sandbox and the real system; other use-cases want the ability to change the layout of the filesystem for processes inside the sandbox, but do not aim to be a security boundary. As a result, the level of protection between the sandboxed processes and the host system is entirely determined by the arguments passed to bubblewrap.

...

> bubblewrap works by creating a new, completely empty, mount namespace where the root is on a tmpfs that is invisible from the host, and will be automatically cleaned up when the last process exits. You can then use commandline options to construct the root filesystem and process environment and command to run in the namespace.

via [b0rk](https://social.jvns.ca/@b0rk/110618354024355244), who has a [blog post about the use case here](https://jvns.ca/blog/2021/09/24/new-tool--an-nginx-playground/)