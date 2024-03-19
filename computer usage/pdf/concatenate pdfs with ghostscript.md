`brew install gs` to get it if you don't have it already, then:

`gs -q -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=combined.pdf one.pdf two.pdf three.pdf [...]`

- `-q`: quiet, don't write to stdout
- `-dNOPAUSE`: `Disables the prompt and pause at the end of each page`
	- not sure why anybody would want a prompt at the end of each page, but I also don't understand ghostscript broadly
- `BATCH`: the manual doesn't mention it
- for `-sDEVICE`, the manual says `You can also check the set of available devices from within Ghostscript: invoke Ghostscript and type 'devicenames =='`
	- but it doesn't mention pdfwrite particularly
	- the devicenames list is extremely cryptic

I got the command from [stack overflow](https://apple.stackexchange.com/a/293198)