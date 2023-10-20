https://github.com/moretension/duti

> duti is a command-line utility capable of setting default applications for various document types on [macOS](https://www.apple.com/macos/), using Apple's [Uniform Type Identifiers](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_intro/understand_utis_intro.html) (UTI). A UTI is a unique string describing the format of a file's content. For instance, a Microsoft Word document has a UTI of `com.microsoft.word.doc`. Using `duti`, the user can change which application acts as the default handler for a given UTI.

example usage - I want to set [[IINA]] to be the default player for webm files. First, check what the current setting is:
```shell
$ duti -x webm
Chromium
/Applications/Chromium.app
org.chromium.Chromium
```

to change it, I need the bundle id of iina. Googling suggests that `mdls` is the tool I want:

```shell
$ mdls -name kMDItemCFBundleIdentifier -r /Applications/IINA.app 
com.colliderli.iina
```

Now I can set `IINA` to be the opener for webm files with:

```
$ duti -s com.colliderli.iina webm all
```

Unfortunately, the tool has no documentation - it's a short C file though.

