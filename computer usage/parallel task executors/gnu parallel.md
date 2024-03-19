https://www.gnu.org/software/parallel/

An example usage: `cat urls.txt | parallel --gnu "wget -nc -P images {}"`

That's from my command history, but it's probably better to use [[curl#Download files in parallel]] which is built in to curl. I have no idea why I used the `--gnu` option, and the manual doesn't clarify its usage. Probably I just copy-pasted from stack overflow.

I have usually found gnu parallel pretty painful to use, and try to avoid it.