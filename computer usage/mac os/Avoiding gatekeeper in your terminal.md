---
created: 2025-09-04T17:30:46.789Z
updated: 2025-09-04T17:30:46.789Z
---
To avoid Gatekeeper slowdowns in your terminal, add it as a "Developer Tool" in "Privacy and Security" settings in the System Settings app:

![[Pasted image 20250904133152.png]]

That will prevent Gatekeeper from running on every app you launch.

via [this article](https://nnethercote.github.io/2025/09/04/faster-rust-builds-on-mac.html) where the author investigated build slowdowns due to Gatekeeper. There [is a comment](https://news.ycombinator.com/item?id=24394150) on news.yc that suggests you may need to run `sudo spctl developer-mode enable-terminal` to enable that category

**TODO**: I really want to be able to add apps to this category with a command line program - anybody know how to do that?