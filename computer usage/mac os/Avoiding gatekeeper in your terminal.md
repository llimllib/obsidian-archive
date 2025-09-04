---
created: 2025-09-04T17:30:46.789Z
updated: 2025-09-04T17:30:46.789Z
---
To avoid Gatekeeper slowdowns in your terminal, add it as a "Developer Tool" in "Privacy and Security" settings in the System Settings app:

![[Pasted image 20250904133152.png]]

That will prevent Gatekeeper from running on every app you launch.

via [this article](https://nnethercote.github.io/2025/09/04/faster-rust-builds-on-mac.html) where the author investigated build slowdowns due to Gatekeeper. There [is a comment](https://news.ycombinator.com/item?id=24394150) on news.yc that suggests you may need to run `sudo spctl developer-mode enable-terminal` to enable that category.

I've added it to my [mac setup script](https://gist.github.com/llimllib/3fc4fefcfc0152dad8c58201246d8802#file-install-sh-L201-L204)

**TODO**: I really want to be able to add apps to this category with a command line program - anybody know how to do that?

Some github sleuthing later reveals:

- To get an app's bundle specifier, use `mdls -name kMDItemCFBundleIdentifier $APP_NAME`
- This pair of commands would _probably_ insert Alacritty into the correct section, but is not enabled unless SIP is disabled:

```bash
sudo tccutil --service "kTCCServiceDeveloperTool" --insert "org.alacritty"
sudo tccutil --service "kTCCServiceDeveloperTool" --enable "org.alacritty"
```

Something that's neat is that you can see what's in that table via sqlite:

```bash
$ sudo sqlite3 /Library/Application\ Support/com.apple.TCC/TCC.db << 'EOF'
.headers on
.mode column
select service, client, last_modified from access where service='kTCCServiceDeveloperTool';
EOF
service                   client                 last_modified
------------------------  ---------------------  -------------
kTCCServiceDeveloperTool  com.apple.Terminal     1757006811   
kTCCServiceDeveloperTool  com.googlecode.iterm2  1757006821   
kTCCServiceDeveloperTool  com.mitchellh.ghostty  1757006816   
kTCCServiceDeveloperTool  net.kovidgoyal.kitty   1757006809 
```