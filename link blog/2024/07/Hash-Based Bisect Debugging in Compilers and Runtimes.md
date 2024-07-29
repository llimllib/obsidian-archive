---
created: 2024-07-29T12:10:26.575Z
updated: 2024-07-29T12:10:26.575Z
---
https://research.swtch.com/bisect

Russ Cox writes about a new tool he, Keith Randall, and David Chase made, which effectively allows him to run `git bisect` against the go interpreter, but bisecting across the program instead of across commit history.

> That is, we can run binary search on a different axis: over the program’s code, not its version history. We’ve implemented this search in a new tool unimaginatively named `bisect`. When applied to library function behavior like the timer change, bisect can search over all stack traces leading to the new code, enabling the new code for some stacks and disabling it for others. By repeated execution, it can narrow the failure down to enabling the code only for one specific stack

```
% go install golang.org/x/tools/cmd/bisect@latest
% bisect -godebug asynctimerchan=1 go test -count=5
...
bisect: FOUND failing change set
--- change set #1 (disabling changes causes failure)
internal/godebug.(*Setting).Value()
    /Users/rsc/go/src/internal/godebug/godebug.go:165
time.syncTimer()
    /Users/rsc/go/src/time/sleep.go:25
time.NewTimer()
    /Users/rsc/go/src/time/sleep.go:145
time.After()
    /Users/rsc/go/src/time/sleep.go:203
rsc.io/tmp/timertest/retry.Do()
    /Users/rsc/src/rsc.io/tmp/timertest/retry/retry.go:37
rsc.io/tmp/timertest/retry.TestDo()
    /Users/rsc/src/rsc.io/tmp/timertest/retry/retry_test.go:63
```

> One of the hardest things about debugging is running a program backward: there’s a data structure with a bad value, or the control flow has zigged instead of zagged, and it’s very difficult to understand how it could have gotten into that state. In contrast, this bisect tool is showing the stack at the moment just before things go wrong: the stack identifies the critical decision point that determines whether the test passes or fails. In contrast to puzzling backward, it is usually easy to look forward in the program execution to understand why this specific decision would matter. Also, in an enormous code base, the bisection has identified the specific few lines where we should start debugging. We can read the code responsible for that specific sequence of calls and look into why the new timers would change the code’s behavior. 

## Relationship to test case minimization

He discusses [later on in the piece](https://research.swtch.com/bisect#example) why they can't use naïve bisection by splitting function sets in half, and instead have to search over list prefixes.

This reminds me strongly of David MacIver's work on minimization, most recently with [[shrinkray]]. I'd have to think harder about it to figure out exactly how it's connected.

## Flaky cases kill bisect

> One interesting thing we learned while working on bisect is that it is important to try to detect flaky tests. Early in debugging loop change failures, bisect pointed at a completely correct, trivial loop in a cryptography package. At first, we were very scared: if that loop was changing behavior, something would have to be very wrong in the compiler. We realized the problem was flaky tests. A test that fails randomly causes bisect to make a random walk over the source code, eventually pointing a finger at entirely innocent code

## Using it yourself

The `bisect` tool is not specialized to the go compiler; it works by setting environment variables (if I understand correctly), and expecting responses from the program in a specific format. Documentation and installation instructions are [here](https://pkg.go.dev/golang.org/x/tools/cmd/bisect)