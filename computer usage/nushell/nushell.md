---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/nushell/nushell
https://www.nushell.sh/book/quick_tour.html

Got inspired to try this again today because of how annoying it was to head [[parquet]] files in bash, while it's built-in to nushell.

## commands

`ls | sort-by size` to... well I think you can guess from reading it

```
$ echo "https://www.nushell.sh/book/quick_tour.html" | url host
www.nushell.sh
```

Handy! I've often complained about how difficult this is in bash-land

I'm going to trip up on stuff like this:

```
For example, in bash, you might use:

> echo "hello" > output.txt

In Nushell, we use the `>` as the greater-than operator. This fits better with the language aspect of Nushell. Instead, you pipe to a command that has the job of saving content:

> echo "hello" | save output.txt

The way Nushell views data is that data flows through the pipeline until it reaches the user or is handled by a final command.
```

`ls **/*.png | get 0.name`:  list all the PNG files in this directory and its subdirectories, and print the name of the first one

`ls **/*.png | get 0.name | each { |f| imgcat $f }` I feel like there must be a smoother way to do this, but this takes the result of the previous command and cats it to the terminal window with `imgcat`

ah ha! the `$in` variable represents the input to the command, so we can simplify that to:

`ls **/*.png | get 0.name | imgcat $in`

```
open foo.db | query db "select * from some_table"
```

nu natively supports querying [[sqlite]]! Neat.

- you can't use `\` as a line continuation, you need to enclose your statement in curly braces