---
created: 2024-09-16T14:10:57.610Z
updated: 2024-09-16T14:10:57.610Z
---
- install zig 0.13
- `zig init`
	- creates: 
- tried: `zig fetch --save https://github.com/ggerganov/whisper.cpp/archive/refs/tags/v1.6.2.tar.gz`
	- that didn't work, complained that there's no name given for the library in build.zig
- docs suggested changing `--save` to `--save=whisper.cpp`, so that's what I did
	- that downloaded the tarball and gave it a hash
```
	    .dependencies = .{
        .@"whisper.cpp" = .{
            .url = "https://github.com/ggerganov/whisper.cpp/archive/refs/tags/v1.6.2.tar.gz",
            .hash = "1220f07aacf48a06ba54a877958d50a05937b03c63a0726b4491c8c9821378b0670b",
        },
    },
```