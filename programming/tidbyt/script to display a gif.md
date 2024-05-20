---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
you program the tidbyt with [[Starlark]]. Here's a bash script I use for displaying a gif image on mine:
	- you'll need [pixlet](https://github.com/tidbyt/pixlet) and [[gifsicle]] installed

```bash
#!/usr/bin/env bash
set -euo pipefail

function usage {
    cat <<"EOF"
gif.sh [-rv] image.gif
display image.gif on your tidbyt. Assumes you have `pixlet` installed, and that
the device you want to display it on is the first in the list of `pixlet
devices`
FLAGS:
  -r: resize the gif to the size of the tidbyt screen (64x32) using `gifsicle`
  -v: verbose mode
EOF
    exit 1
}

RESIZE=

while true; do
    case $1 in
        -v | --verbose)
            set -x
            shift
            ;;
        -r | --resize)
            RESIZE=true
            shift
            ;;
        *)
            break
            ;;
    esac
done

if [[ -z $1 ]]; then
    usage
fi

gif=$1
if [[ -n $RESIZE ]]; then
    sized_gif="$(mktemp).gif"
    gifsicle --resize 64x32 "$gif" > "$sized_gif"
    gif=$sized_gif
fi

delay=1000
tmpfile="$(mktemp -t star).star"
starout=$(mktemp -t starout)
tee "$tmpfile" << EOF &> /dev/null
load("render.star", "render")
load("encoding/base64.star", "base64")
image=base64.decode('$(base64 -i "$gif")')
def main():
    return render.Root(
        render.Image(src=image),
        delay=$delay,
    )
EOF

pixlet render -o "$starout" "$tmpfile"
pixlet push "$(pixlet devices | awk 'NR==1{print $1}')" "$starout"
```