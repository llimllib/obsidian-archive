I had cause to figure out how to do this today. The only third-party tool is [schollz/progressbar](https://pkg.go.dev/github.com/schollz/progressbar/v3#section-readme), which I used in the most absolutely basic way, straight from its manual.

### Updated: version 2

- Thanks to [Carl Johnson](https://mastodon.social/@carlmjohnson/110622622241518771) for proposing this improvement
	- Create a signal context that cancels if a signal is received
	- Start the download to a "part" file that contains a partial download, and use a `defer` to remove it
		- The defer is vital because the `defer` will fire on an interrupt and it means we don't have to have an out-of-band "done" signal like in version 1
	- Check the error on `io.Copy` to see if it was a context cancellation
		- if it was, exit quietly
		- if it wasn't, handle errors as normal
	- When the download is complete, move the part file to the final filename

```go
// create a context that will cancel on interrupt. defer'ing stop
// guarantees that when the function exits nothing will be listening
// for the signal any longer
ctx, stop := signal.NotifyContext(context.Background(), os.Interrupt, syscall.SIGTERM)
defer stop()

// prepare the download. Note that we're now using `NewRequestWithContext`
src := "https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml"
uri := fmt.Sprintf("%s-%s.bin", src, name)
req := must(http.NewRequestWithContext(ctx, "GET", uri, nil))
resp := must(http.DefaultClient.Do(req))
defer resp.Body.Close()

// download to a `<filename>.part` file until the download is successfully complete
inProgressDownloadName := outputFile + ".part"
out := must(os.Create(inProgressDownloadName))
defer os.Remove(inProgressDownloadName)

bar := progressbar.DefaultBytes(
	resp.ContentLength,
	fmt.Sprintf("downloading %s model", yellow(name)),
)

// Check for context.canceled, so that we don't output an unsightly error if
// a user cancels the program. If it's any other error, handle as normal
_, err := io.Copy(io.MultiWriter(out, bar), resp.Body)
if err != nil {
	if err != context.Canceled {
		fmt.Println(err)
		panic(err)
	} else {
		os.Exit(1)
	}
}

// Download complete. rename the <filename>.part file -> <filename>
must_(os.Rename(inProgressDownloadName, outputFile))

fmt.Println(yellow("download complete"))
```

[version 2 in context](https://github.com/llimllib/blisper/blob/42b39bbaba00fe92ad616c4dbec446f8390a5492/main.go#L121-L153)

### version 1

The procedure for handling interrupt is to:
- create a "done" channel to signal a complete download
- run a gofunc which attaches `signal.Notify` to an interrupt channel, then waits on it as well as the done channel
	- handle the interrupt channel by deleting the partially-downloaded file
	- handle the done channel by clearing the interrupt handle
		- if you don't do this (I didn't on my first try), then golang will be futilely signalling the channel that is no longer attached to anything instead of handling interrupts normally

```go
src := "https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml"
uri := fmt.Sprintf("%s-%s.bin", src, name)
req := must(http.NewRequest("GET", uri, nil))
resp := must(http.DefaultClient.Do(req))
defer resp.Body.Close()

out := must(os.Create(outputFile))
defer out.Close()

bar := progressbar.DefaultBytes(
	resp.ContentLength,
	fmt.Sprintf("downloading %s model", yellow(name)),
)

// handle a sigint while we're downloading
done := make(chan bool)
go func() {
	sigchan := make(chan os.Signal, 1)
	signal.Notify(sigchan, os.Interrupt, syscall.SIGTERM)
	select {
	case <-sigchan:
		// ignore errors here, we've been interrupted and we're on
		// best-effort at this point. Try to remove the partial download
		out.Close()
		os.Remove(outputFile)
		os.Exit(1)
	case <-done:
		// the download finished, remove the handler and continue
		signal.Stop(sigchan)
		return
	}
}()

must(io.Copy(io.MultiWriter(out, bar), resp.Body))

// tell the interrupt handler we finished the download, it doesn't need to
// run any longer
done <- true

fmt.Printf("%s\n", yellow("download complete"))
```

You can see it [in context here](https://github.com/llimllib/blisper/blob/feeb15f9b5ab5e92551f34d24188c85308f2fa00/main.go#L117-L159)

(if you were curious, `must` is a function that accepts a value and an error, and returns the value if there wasn't an error:

```go
// must accepts a value and an error, and returns the value if the error is
// nil. Otherwise, prints the error and panics
func must[T any](t T, err error) T {
	if err != nil {
		fmt.Println(err)
		panic(err)
	}
	return t
}
```

I'd label my usage of it as experimental, but I like it so far. Somewhat similar to zig's `try`.)