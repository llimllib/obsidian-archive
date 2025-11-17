---
created: 2025-11-17T21:20:26.524Z
updated: 2025-11-17T21:20:26.524Z
---
https://github.com/Mic92/strace-macos

> A clone of the strace command for macOS

> - **Works with SIP enabled** - Unlike `dtruss`, doesn't require disabling System Integrity Protection
> - **Pure Python implementation** - No kernel extensions or compiled components
> - **Multiple output formats** - JSON Lines and strace-compatible text output
> - **Syscall filtering** - Filter by syscall name or category (`-e trace=file`, `-e trace=network`)
> - **Symbolic decoding** - Automatically decodes flags, error codes, and struct fields
> - **Color output** - Syntax highlighting when output is a TTY
> - **Summary statistics** - Time/call/error counts with `-c`

## Installation

Since it isn't on homebrew or anything, I tried running it with `uv`, but unfortunately this failed:

<details>
<summary>failure output</summary>

```
$ uvx --from git+https://github.com/Mic92/strace-macos strace git status          
Traceback (most recent call last):
  File "/Users/llimllib/.cache/uv/archive-v0/XfeZEv8TRktvHK3dWL1Ne/bin/strace", line 12, in <module>
    sys.exit(main())
             ^^^^^^
  File "/Users/llimllib/.cache/uv/archive-v0/XfeZEv8TRktvHK3dWL1Ne/lib/python3.12/site-packages/strace_macos/__main__.py", line 85, in main
    tracer = Tracer(
             ^^^^^^^
  File "/Users/llimllib/.cache/uv/archive-v0/XfeZEv8TRktvHK3dWL1Ne/lib/python3.12/site-packages/strace_macos/tracer.py", line 75, in __init__
    self.lldb = load_lldb_module()
                ^^^^^^^^^^^^^^^^^^
  File "/Users/llimllib/.cache/uv/archive-v0/XfeZEv8TRktvHK3dWL1Ne/lib/python3.12/site-packages/strace_macos/lldb_loader.py", line 89, in load_lldb_module
    raise LLDBLoadError(msg)
strace_macos.exceptions.LLDBLoadError: Failed to load LLDB Python module.
Make sure you're running with system Python (/usr/bin/python3) and have Xcode Command Line Tools installed.

To install Xcode Command Line Tools:
  xcode-select --install
```

</details>

I suspect this might be because `uv` is installed with a homebrew python, not the system python, but that's just a guess.

After installing the recommended way with the system python, I was able to use it:

<details>
<summary>success output</summary>

```
$ /usr/bin/python3 -m pip install --user git+https://github.com/Mic92/strace-macos
# installs to ~/Library/Python/3.9/bin which isn't in my $PATH, so I call it directly:
$ ~/Library/Python/3.9/bin/strace git status  
access("/AppleInternal/XBS/.isChrooted", F_OK) = -1 EPERM (Operation not permitted)
getpid() = 53169
shm_open("com.apple.featureflags.shm", 0, 6485946900) = 3
fstat(3, {st_dev=0, st_mode=00|0644, st_nlink=0, st_ino=0, st_uid=0, st_gid=0, st_rdev=0, st_atimespec_sec=0, st_mtimespec_sec=0, st_ctimespec_sec=0, st_birthtimespec_sec=0, st_size=32768, st_blocks=0, st_blksize=0, st_flags=0, st_gen=0}) = 0
mmap(0x0, 32768, PROT_READ, MAP_SHARED, 3, 0) = 4298768384
close(3) = 0
getpid() = 53169
getpid() = 53169
ioctl(2, FIODTYPE, 0x103) = 0
mprotect(0x100a38000, 16384, PROT_NONE) = 0
mprotect(0x100e3c000, 16384, PROT_NONE) = 0
mprotect(0x1007e0000, 16384, PROT_READ) = 0
getpid() = 53169
issetugid() = 0
getpid() = 53169
getpid() = 53169
getattrlist("/opt/homebrew/bin/git", 0x16fdfb1e0, 0x16fdfb1fc, 1036, 0) = 0
access("/opt/homebrew/Cellar/git/2.51.2/bin", R_OK) = 0
open("/opt/homebrew/Cellar/git/2.51.2/bin", O_RDONLY, 040051174760) = 3
# etc etc etc
```

</details>

## Usage

A while ago, [on lobste.rs](https://lobste.rs/c/goo2av), `simonw` asked how to see what files `git status` is touching:

> I've been trying to find a reliable recipe for running short-lived commands like `git status` and seeing which files they touch while they are running.

and I suggested an [[eslogger]] solution. Here it is reimplemented in `strace`, which allows us to avoid `sudo` usage, and also to do what we want much more directly

```
$ ~/Library/Python/3.9/bin/strace git status 2>&1 | rg '^(?:access|open)'
access("/AppleInternal/XBS/.isChrooted", F_OK) = -1 EPERM (Operation not permitted)
access("/opt/homebrew/Cellar/git/2.51.2/bin", R_OK) = 0
open("/opt/homebrew/Cellar/git/2.51.2/bin", O_RDONLY, 040045634760) = 3
open("/opt/homebrew/Cellar/git/2.51.2/bin/Info.plist", O_RDONLY, 00) = -1 EPERM (Operation not permitted)
access("/opt/homebrew/Cellar/git/2.51.2/bin", R_OK) = 0
open("/opt/homebrew/Cellar/git/2.51.2/bin", O_RDONLY, 040045636420) = 3
open("/opt/homebrew/Cellar/git/2.51.2/bin/Info.plist", O_RDONLY, 00) = -1 EPERM (Operation not permitted)
access("/opt/homebrew/Cellar/git/2.51.2/bin", R_OK) = 0
open("/opt/homebrew/Cellar/git/2.51.2/bin", O_RDONLY, 040045626040) = 3
open("/opt/homebrew/Cellar/git/2.51.2/bin/Info.plist", O_RDONLY, 00) = -1 EPERM (Operation not permitted)
```

cf [[debugging os x]]