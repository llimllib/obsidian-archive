https://github.com/jpmens/jo

> a small utility to create JSON objects

```shell
$ jo -p name=jo n=17 parser=false
{
    "name": "jo",
    "n": 17,
    "parser": false
}
```

> or arrays

```shell
$ seq 1 10 | jo -a
[1,2,3,4,5,6,7,8,9,10]
```

neat! Useful with curl, like `jo type=message envelope=$(jo sender=me@me.com subject=hi) | curl --json @- httpbingo.org/anything`