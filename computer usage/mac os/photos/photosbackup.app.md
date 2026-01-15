---
created: 2026-01-12T14:41:58.027Z
updated: 2026-01-12T14:41:58.027Z
---
https://photosbackup.app

> Back up your **entire photo library** to any storage location, including external drives and network locations like NAS devices. Supports iCloud and **all media types** such as videos, live photos, portraits, slo-mo, and more and preserves all **non-destructive edits, albums, locations, and timestamps** . Backups can be **restored directly into a photo library**while maintaining all metadata.

via [news.yc](https://news.ycombinator.com/item?id=46578921), where the [author says](https://news.ycombinator.com/item?id=46581764):

> HN disclosure: I’m the author of Photos Backup Anywhere, but this thread mirrors the exact issues that pushed me to write it.
> 
> One thing that surprised me when digging into Apple Photos is how much state isn’t represented by just files-on-disk. Albums, Live Photos (paired assets), bursts, slo-mo, edits, and even “simple” things like adjusted capture dates are all tracked separately, and most export/backup tools end up flattening or partially reconstructing that on restore.
> 
> The approach I took was to treat Photos as the source of truth and verify restored items against it, rather than assuming filesystem metadata is enough. As far as I know, this is the only tool that restores albums and correctly round-trips all Photos item types while preserving location data, creation dates, and modification dates when restoring back into Photos.
> 
> Project page is here if it’s useful: [https://photosbackup.app/](https://photosbackup.app/)
> 
> Happy to explain details if anyone’s curious — there are a lot of sharp edges in Photos once you go beyond “export originals”.