https://jsonnet.org/

> A configuration language for app and tool developers

> - Generate config data
> - Side-effect free
> - Organize, simplify, unify
> - Manage sprawling config

> A simple extension of JSON

> - Open source (Apache 2.0)
> - Familiar syntax
> - Reformatter, linter
> - Editor & IDE integrations
> - Formally specified

---

[here's a good article arguing](https://leebriggs.co.uk/blog/2019/02/07/why-are-we-templating-yaml) for its usage, "Why are we templating YAML?"

> firstly, let's define some jsonnet:

```
{
  image: std.extVar('image'),
}
```

> Then, we can generate it using the Jsonnet command line tool, passing in the external variable as we need to:

```
jsonnet image.jsonnet -V image="my-image"
{
   "image": "my-image"
}
```

I might try this out as a command-line template language