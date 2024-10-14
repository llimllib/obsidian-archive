---
created: 2024-10-14T11:13:21.334Z
updated: 2024-10-14T11:13:21.334Z
---
https://sxlijin.github.io/2024-10-09-node-stdout-disappearing-bytes

`process.stdout.write` presents an interface that implies that it's sync, and I had assumed that it was. However, the [docs say](https://nodejs.org/api/process.html#a-note-on-process-io):

> Writes may be synchronous depending on what the stream is connected to and whether the system is Windows or POSIX:
> - Files: _synchronous_ on Windows and POSIX
> - TTYs (Terminals): _asynchronous_ on Windows, _synchronous_ on POSIX
> - Pipes (and sockets): _synchronous_ on Windows, _asynchronous_ on POSIX

In the [news.yc comments](https://news.ycombinator.com/item?id=41828542), user `jitl` provides this clever bit for how they ensured that stdout and stderr flush completely in their internal tools:

```js
function flushWritableStream(stream: NodeJS.WritableStream) {
      return new Promise(resolve => stream.write("", resolve)).catch(
        handleFlushError,
      )
    }
    
    /**
     * In NodeJS, process.stdout and process.stderr behave inconsistently depending on the type
     * of file they are connected to.
     *
     * When connected to unix pipes, these streams are *async*, so we need to wait for them to be flushed
     * before we exit, otherwise we get truncated results when using a Unix pipe.
     *
     * @see https://nodejs.org/api/process.html#process_a_note_on_process_i_o
     */
    export async function flushStdoutAndStderr() {
      await Promise.all([
        flushWritableStream(process.stdout),
        flushWritableStream(process.stderr),
      ])
    }

    /**
     * If `module` is the NodeJS entrypoint:
     *
     * Wait for `main` to finish, then exit 0.
     * Note that this does not wait for the event loop to drain;
     * it is suited to commands that run to completion.
     *
     * For processes that must outlive `main`, see `startIfMain`.
     */
    if (require.main === module) {
      await main(argv)
      await flushStdoutAndStderr()
      setTimeout(() => process.exit(0))
    }
```