---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/zcutlip/prefsniff

> `prefsniff` is a utility to watch macOS plist files for changes, and then autogenerate the `defaults` command to apply those changes. Its intended use is to have `prefsniff` watch a plist file while setting a system or application preference. The resulting defaults command can then be added to a shell script or incorporated into a configuration management system such as Ansible.

This could be useful for improving my [install script](https://gist.github.com/llimllib/c4dd0a98a426022b0365d4c0a9090460); I have lots of settings in there, but it's missing lots of settings too.