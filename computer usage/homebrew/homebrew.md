---
created: 2024-06-07T00:59:32.219Z
updated: 2024-07-31T12:51:31.477Z
---
https://brew.sh
https://github.com/Homebrew/brew
https://github.com/Homebrew/homebrew-core
https://github.com/Homebrew/homebrew-cask

## finding out what packages depend on a given package

```
brew uses --installed openssl@1.1
```

## to see a dependency tree for a given package

```
brew deps --tree glslviewer
```