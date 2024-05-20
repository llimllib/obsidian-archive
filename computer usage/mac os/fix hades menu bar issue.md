---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Find the plist for hades; mine was at `~/Library/Application Support/Steam/steamapps/common/Hades/Game.macOS.app/Contents/Info.plist`, and edit it to add this key:

```
    <key>LSUIPresentationMode</key>
    <integer>3</integer>
```

hmmm this did not work. (I tried 4 too, as suggested in some video, also didn't work)