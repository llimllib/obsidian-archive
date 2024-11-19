---
updated: 2024-11-18T14:19:07.037Z
created: 2023-10-20T13:54:09Z
---
https://vorpus.org/blog/notes-on-structured-concurrency-or-go-statement-considered-harmful/

Argument from the creator of [trio](https://github.com/python-trio/trio) that the "go" statement (which from the article's perspective is the same as every other new thread primitive) can be improved by using an abstraction he calls a "nursery" which does not end until the called functions do.

As I understand them, if we do:

```go
go someProcess(fileHandle);
someOtherStuff();
```

we're left without knowing lots of basic things about `fileHandle` - has it been modified? closed? can we close it?

(the article does not engage with or does not consider important the idea that processes might only communicate via messages)

So they propose the `nursery` abstraction, in python for their examples. Tranlsated into a hypothetical go, it might look like

```go
var nursery Nursery
fileHandle := os.Open("file.txt")

err := with(nursery) {
  go someProcess(fileHandle);
  go someOtherProcess(...);
}
if err != nil {
  panic(err);
}

fmt.Printf("program proceeds here only after both processes finish");
// ex we know we can safely close the fileHandle
os.Close(fileHandle)
```

Where the important properties of `with` are that it enables resource collection and error handling, since control flow is linear in the scope of this function.

Links to [[oklog-run]] as maybe the closest thing implementable in go

See [[flowmatic]] for a library that attempts to improve the go statement with similar ideas