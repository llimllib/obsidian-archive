https://curl.se

I use curl very frequently, I'm kind of shocked I didn't have a page for it yet.

----

## Download files in parallel

I have previously done this with wget, xargs, or both. Today I decided to figure out how to use curl's [native parallel download support](https://everything.curl.dev/cmdline/urls/parallel).

The impetus for the test was wanting to download all the images from the [planet.com
gallery](https://www.planet.com/gallery/) to use as background images, and the full script is [here](https://github.com/llimllib/personal_code/blob/master/bash/download_planetcom_gallery/dl.sh).

The gist is that you create a series of commands for curl to run (curl has no support for files containing newline-separated URLs) that looks like this:

```
url = https://example.com/uri/1

url = https://example.com/uri/2
```

and so on and so forth. You can specify additional options; it's [documented here](https://everything.curl.dev/cmdline/configfile), but for this task I had no need to do so.

Once I generated this file, I downloaded it with:

```sh
curl --remote-name-all --output-dir images \
    --parallel --parallel-immediate --parallel-max 5 \
    --continue-at - \
    --write-out "%{response_code} -> %{filename_effective}\n" \
    --config "$URLS"
```

The parallel options are documented [here](https://everything.curl.dev/cmdline/urls/parallel); I used `--continue-at -` to prevent curl from re-downloading files; it lacks the ability to do so by filename so this does it by requests to the server instead. (It stinks that curl lacks an equivalent of wget's `--no-clobber`)

The [`--write-out`](https://everything.curl.dev/usingcurl/verbose/writeout) bit tells curl to output something for each file downloaded; read the docs for the options of what you can write.

----

[curl converter](https://curlconverter.com) is handy for turning curl commands into various other formats

----

[websocket in curl](https://curl.se/docs/websocket.html) is a new-ish capability. Currently only usable via the API, but command line usage is planned.

## caching

TIL that you can use `--etag-compare` and `--etag-save` to download files with curl only if the file has changed. So,

```
curl --etag-compare etag.txt --etag-save etag.txt 'https://csvbase.com/ngkabra/Statistics' -O
```

says: 
- compare the etag on the server to `etag.txt`
- save the etag from the server if the file is downloaded as `etag.txt`
- download https://csvbase.com/ngkabra/Statistics
- `-O` means "save the file with a filename similar to the one on the remote", in this case `Statistics`

The result is that curl will download the file only if it hasn't already been downloaded, or if the remote etag changes.

Via [Why my favourite API is a zipfile on the European Central Bank's website](https://csvbase.com/blog/5), more specifically the [hn comments](https://news.ycombinator.com/item?id=37527688) (but the post is worth reading)

### or -z

curl also has the `-z` option, which accepts a filename. If you give it a date it can parse, or a filename, it will only download the remote file if newer than `-z`. So this command means "only download the zip file if it's newer than the `/tmp/euro.zip` file we have on disk":

`curl -s -o /tmp/euro.zip -z /tmp/euro.zip https://www.ecb.europa.eu/stats/eurofxref/eurofxref-hist.zip`