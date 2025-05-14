https://github.com/BurntSushi/biff
https://github.com/BurntSushi/biff/blob/master/GUIDE.md

A CLI date manipulation tool from the great BurntSushi (author of [[ripgrep]], among other stuff).

I had written my own tool, `,time` ([source here](https://github.com/llimllib/personal_code/blob/eafbb593333e61e17b594fb52651f2a031f1c836/homedir/.local/bin/%2Ctime)), which without arguments prints the time in various formats:

```
$ ,time
ts seconds: 1747098407.0
ts ms:      1747098407000
Local:      2025-05-12 21:06:47 EDT
UTC:        2025-05-13 01:06:47 UTC
```

or if you give it an argument, it tries to parse it:

```
$ ,time March 12 2025
ts seconds: 1741752000.0
ts ms:      1741752000000
Local:      2025-03-12 00:00:00 EDT
UTC:        2025-03-12 04:00:00 UTC
```

We can express each of those in biff:

```shell
$ biff time fmt -f '%s' now
1747100661

# biff doesn't support milliseconds since the epoch, so we can 
# calculate it, round it to milliseconds, then strip the ms. A 
# bit awkward.
# https://github.com/BurntSushi/biff/issues/3
$ biff span until -r '1970-01-01T00Z' now | 
    biff span round -l ms -s ms | 
    sed 's/ms//'   
1747246662147

# by default, biff does not try to guess your desired time locale, 
# and prints a rather ugly default locale
$ biff time fmt -f '%c' now                  
2025 M05 14, Wed 14:20:16

# so you have to ask it specifically to use your locale via the
# BIFF_LOCALE variable
$ BIFF_LOCALE=en-US biff time fmt -f '%c' now
Wed, May 14, 2025, 2:20:13 PM EDT

# to get GMT time, you need to set the TZ variable to a timezone, 
# and the locale variable for date format
$ BIFF_LOCALE=en-US TZ=etc/GMT biff time fmt -f '%c' now
Wed, May 14, 2025, 6:28:09 PM GMT
```

But each of them is pretty awkward, so I was initially excited to replace my tool with this one but I think I'll keep it around for now.

- [here is documentation on the full list of supported time formatting options](https://github.com/BurntSushi/biff/blob/884b273d9d777fe74f7abc39d6f13a1807f83da0/src/args/flags.rs#L209)