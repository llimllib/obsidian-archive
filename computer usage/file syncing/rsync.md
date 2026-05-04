---
updated: 2026-05-02T17:27:13.197Z
created: 2023-10-20T13:54:09Z
---
https://rsync.samba.org

The classic file syncing program

----

for a useful progress display without echoing every file to the terminal, try `--info=progress2`:

for example: `rsync -a --info=progress2 ../branch/node_modules ./node_modules` won't print every file it copies in the node_modules dir, which is enormous, but will print useful progress.

---

How I sync my local music directory with my file server:

```bash
#!/usr/bin/env bash
SOURCE="/Users/llimllib/Music/"
DEST="/Volumes/music"

# Check if destination exists
if [ ! -d "$DEST" ]; then
    echo "Error: Destination directory $DEST does not exist"
    echo "Is the volume mounted?"
    exit 1
fi

# Sync with progress
rsync -avh --progress \
  --exclude='Music/' --exclude='GarageBand/' --exclude 'Audio Music Apps/' \
  "$SOURCE" "$DEST"
```