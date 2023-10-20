I downloaded a bunch of files and accidentally wrote them with the file `some_file_name.mp3?html_garbage=goes_here`, and wanted to remove the suffix from all of them. This simple loop did the trick:

```bash
#!/usr/bin/env bash
for i in *.mp3*; do 
  mv "$i" "${i%\?*}"
done
```