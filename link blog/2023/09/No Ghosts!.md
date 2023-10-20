https://blog.sunfishcode.online/no-ghosts/ via [[Understanding WASM Part 3 - you are here]]

> By “ghost” here, I mean any situation where resources are referenced by _plain data_.

> And by “plain data” here, I mean strings, integers, or any other data where independently produced copies of the data are interchangeable. For example, two completely independent parts of a system may create a string with the value `"Purple"`, and the two strings will be interchangeable.

> ...\[when two parts of a system use a `TIMEOUT` environment variable, they] both use the string `"TIMEOUT"` as an identifier to send a message between them. As far as these specific parts of the code know, it's as if the content of the message is carried by a ghost, from one part to the other.

> ...when designing component APIs, we should seek to avoid ghosts where we can, and seek to identify and encapsulate ghosts where we can't.

---
> To avoid ghosts, it's not enough to change the mechanisms. To change the relationships, we need to switch from coarse-grained sharing to fine-grained sharing with handles. Instead of whole filesystems, we should ideally reference specific directories or even individual files, such as like this:

```c
    // Open the file using our own privileges.
    file_handle = open(root_handle, "tmp/file.txt");

    // Instead of passing root_handle and a path, pass
    // *just* the one file handle to the other component.
    process_open_file(file_handle);
```

----

ed: Talking about ghosts in the system highlights the importance of communal knowledge.

The more knowledge and aesthetic you can assume a team shares, the more you can accept "ghosts" in the system without causing undue problems.

The less knowledge, the more carefully you must make explicit every reference.

This means that if you are working on a product for a startup, you may accept ghosts as the cost of doing business: tech debt that speeds you up ("Ghosts are often _convenient_") but will become crufty as new developers come on board and you eventually do not share the same context.

If you're working on a library that you expect many teams to use, you should probably be working hard to prevent ghosts in your API surface from day 1.