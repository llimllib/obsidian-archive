---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
The best way to embed a quote in bash is to use the `$'` syntax:

```
$ echo $'python -c "print(\'hello\')"'
python -c "print('hello')"
```

It lets you use C-style escapes, which otherwise don't work. An SO comment says:

> Since Bash [2.04](http://wiki.bash-hackers.org/scripting/bashchanges) syntax `$'string'` allows a limit set of escapes.

> Since Bash 4.4, `$'string'` also allows the full set of [C-style escapes](https://en.wikipedia.org/wiki/Escape_sequences_in_C#Table_of_escape_sequences), making the behavior differ slightly in `$'string'` in previous versions. (Previously the `$('string')` form could be used.)

## an alternative

If that doesn't work for some reason is to end the string and start another one:

```
$ echo 'python -c "print('\''hello'\'')"'
python -c "print('hello')"
```

Here we have three strings, with an escaped quote between them. They are: `'python -c "print('`, then a quote, then `'hello'`, then a quote, then `')"'`

