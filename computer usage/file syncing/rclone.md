https://rclone.org/
https://github.com/rclone/rclone

Rclone _("rsync for cloud storage")_ is a command-line program to sync files and directories to and from different cloud storage providers.

Written in go, works with many cloud providers. Looks like a neat tool.

----

Just learned that rclone can be [used to mount a filesystem with fuse](https://rclone.org/commands/rclone_mount/), meaning it can be used to replace sshfs as well as replicate that functionality for many other storage systems.