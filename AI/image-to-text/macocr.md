---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Command line utility showing how to use the [VNRecognizeTextRequest](https://developer.apple.com/documentation/vision/vnrecognizetextrequest) API.

Unfortunately doesn't output in a sensible format - outputs a JSON-looking array prefixed with "got page obs is"

In order to build it, I needed to:

```shell
gh repo clone MatthiasWinkelmann/macocr 

# Now when I tried to run "swift build", it threw:
# $ /usr/bin/xcrun --sdk macosx --show-sdk-platform-path
# xcrun: error: unable to lookup item 'PlatformPath' from 
# command line tools installation
# xcrun: error: unable to lookup item 'PlatformPath' in SDK 
# '/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk'

# to fix it, I made sure that xcode was installed by starting
# it up, then:
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer

# now `swift build` works
swift build
swift run
```

The code is extremely simple and can be read in 10 minutes.