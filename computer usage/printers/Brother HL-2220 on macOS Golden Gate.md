---
created: 2026-09-26T19:40:28.802Z
updated: 2026-09-26T19:40:28.802Z
---
Brother's printer driver for the HL-2220 on macOS 27 (Golden Gate) is x86_64 only, I discovered when I tried to print after I upgraded.

To fix it, the agent built me a  driver from [brlaser](https://github.com/pdewacht/brlaser), which restores the printer.

The agent says:

> The HL-2220 is a host-based "GDI" printer — no PostScript, no PCL, no AirPrint/IPP.

To compile the driver, it did:

```sh
git clone --depth 1 https://github.com/pdewacht/brlaser.git
cd brlaser
cmake -B build -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_OSX_ARCHITECTURES=arm64 \
      -DCMAKE_POLICY_VERSION_MINIMUM=3.5
cmake --build build -j8
cd build && ctest            # 4/4 passed
ppdc -d ppd brlaser.drv      # generates ppd/br2220.ppd
```

Build deps came from Homebrew (`cmake`) plus the CLT SDK for `cups/raster.h`.

> [!warning] Two gotchas
> 1. `-DCMAKE_POLICY_VERSION_MINIMUM=3.5` is required — current CMake rejects the
>    project's old `cmake_minimum_required` outright.
> 2. The generated PPD names the filter bare (`rastertobrlaser`), so CUPS looks in
>    `ServerBin` = `/usr/libexec/cups/filter`, which is **read-only under SIP**.
>    Rewrite it to an absolute path in `/usr/local/libexec/cups/filter/`. This is
>    exactly what Brother's own PPD does.

To install it:

```sh
install -d -o root -g wheel -m 755 /usr/local/libexec/cups/filter
install -o root -g wheel -m 755 rastertobrlaser /usr/local/libexec/cups/filter/
install -o root -g wheel -m 644 brlaser-hl2220.ppd \
  /Library/Printers/PPDs/Contents/Resources/
lpadmin -p HL2220_brlaser \
  -v 'usb://Brother/HL-2220%20series?serial=A1N115108' \
  -P /Library/Printers/PPDs/Contents/Resources/brlaser-hl2220.ppd \
  -D 'Brother HL-2220 (brlaser)' -L adama -o printer-is-shared=false -E
```

In the future, to diagnose an error, try `lpstat -l -p <queue>`, which is what the agent used to diagnose the `badarch` error

I probably could have installed rosetta 2 to get it working, but this seems sufficient for now and I can get rid of Brother's driver