---
created: 2025-12-27T22:02:20.089Z
updated: 2025-12-27T22:02:20.089Z
---
https://github.com/rcarmo/PhotosExport

> `PhotosExport` is a small macOS command-line tool that exports **Apple Photos** library assets to the filesystem, and that I developed out of frustration with Shortcuts’ limited (i.e., non-existent) Photos export capabilities and the brokenness of AppleScript-based solutions.

> It is intentionally opinionated:

> - Exports **assets from a complete calendar year** (current year by default).
> - For each asset, exports **all available `PHAssetResource`s** (including originals, `FullSizeRender` resources, Live Photo paired video resources, adjustment data, brush stroke retouches, etc.), when present.
> - Writes into a simple `YYYY/MM` folder hierarchy.
> - Uses a deterministic timestamp-based naming convention.

I can testify to the difficulty of exporting apple's photos, and I look forward to giving this tool a try.

via [mastodon](https://mastodon.social/@rcarmo/115792050482682107)