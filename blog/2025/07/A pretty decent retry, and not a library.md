---
created: 2025-07-19T15:14:41.434Z
updated: 2025-07-19T15:14:41.434Z
---
I'm pretty happy with the [retry function](https://github.com/llimllib/nba_data/blob/dbbed16c1c05a118b98e92da099267f3ffb7a8cd/src/stats.py#L37-L72) I've ended up with for my [nba stats downloader](https://github.com/llimllib/nba_data/):

```python
G = TypeVar("G")

def retry(f: Callable[..., G], **kwargs) -> G:
    """
    Retry a function call with backoff and print out the exceptions raised
    unless they are a timeout.
    """
    i = 0
    while 1:
        try:
            return f(**kwargs)
        except Exception as exc:
            if i > 11:
                raise RetryLimitExceeded(f.__name__, i, kwargs, exc)
            timeout = [1, 2, 5, 10, 15, 20, 25, 25, 25, 50, 50, 100][i]
            i += 1
            print(f"failed {f.__name__}({kwargs}), sleeping {timeout}:\n{exc}")
            # print the traceback unless it's a timeout
            if not isinstance(exc, (ReadTimeout, ReadTimeoutError, TimeoutError)):
                print(traceback.format_exc())
            sleep(timeout)
    # The LSP doesn't detect that this is unreachable: appease it
    raise Exception("this should never happen")
```

## Be explicit

One thing I like about it is that it doesn't calculate a backoff value - it picks from an explicit list of backoffs. 

Before I wrote this one, I had written a bunch of retry functions and always tried to come up with some clever exponential algorithm and do a bit of math. One day I was working with backoffs for my day job in a database context and I decided to go look at [what sqlite uses](https://github.com/sqlite/sqlite/blob/1f436ad563c4f16b94060a1982ae41abac015053/src/main.c#L1709-L1737):

```c
static const u8 delays[] = { 1, 2, 5, 10, 15, 20, 25, 25,  25,  50,  50, 100 };
delay = delays[count];
// ed: That's "sqlite3 OS sleep", not "sqlite 30s sleep"
sqlite3OsSleep(db->pVfs, delay*1000);
```

It's pleasantly [grug-brained](https://grugbrain.dev); why use clever code when simple code do trick?

So I stole the idea and I use it whenever I need a retry function now.
## Don't be generic

The retry function does not allow you to specify your timeouts or configure the list of exceptions that don't get tracebacks or configure the message that gets thrown.

It doesn't support regular args because I only need kwargs in the context I'm using it in.

If I needed to use it again, I'd probably have to modify one or both of those choices. That's OK!

This leads to:
## Don't create a library for small stuff

One instinct for a free software developer, when they have a pleasant battle-tested function, is to make it into a library. The Javascript ecosystem is full of libraries this small or smaller - I could go look and I'm sure I'd find seventeen similar examples of retry libraries.

It feels nice, like you're giving back to the community that you've drawn value from.

But it's a mirage!

The value of having a small function like this in your codebase, where you can see it, read it, and tailor it to suit your needs is greater than the value of having a highly configurable library that's difficult to read and debug.

As the code gets more complex, the weight of that complexity can make it such that it starts to make sense to isolate the code into a library and share it.

I'd like to advocate that people usually underweight how much value there is in having the code included in your application by tailoring it to your application exactly rather than abstracting it into a library.
## Toolboxes, not libraries

For small code tasks like this, it's better to have a toolbox of examples you can pull from and customize.

If I needed retry in a golang or rust program tomorrow, I could easily remember that I've written this code and translate it for use. If I'd instead used a retry library, I'd have to find one in that ecosystem and figure out which library was best, how to use it, and add an external dependency.

This is much of the value that StackOverflow has provided to the world: a giant set of comments containing small, customizable code examples such as this one that solve small problems, which people can copy and modify as they wish.

Given that StackOverflow seems to be dying, I wonder how we could do a better job supporting this "toolbox" type of code?

Would it make sense for language ecosystems to host toolboxes? What if python had a `python.org/examples` library where people can paste code examples with a description and usage guide, and perhaps star them when they find them useful?

Or perhaps we could try to have a sort of "codex" by problem type, where `retry` had a thousand examples in different languages, with different techniques, usages, and lineages?

## postscript

- Kartik Agaram points to [this excellent post](https://akkartik.name/post/four-repos) about four repositories he's created and uses, that he calls "template repositories", similar to the "toolbox" idea