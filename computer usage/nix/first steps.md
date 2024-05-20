---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
my biases: I'm very intrigued by nix but worried that it's a big time sink that's not overall worth the gain for the complexity.

However, I do think it's neat and would like to understand it more. So, onward.

Start a shell with python 3.10 (currently) and ipython:

```
nix-shell -p 'python3.withPackages (p: [p.ipython])'
```

`go` gets me go version 1.18, which as of today is 23 days behind:

```
nix-shell -p 'go'
```

ah ha, but `nix-shell -p 'go_1_19'` gets me the current version:

```
nix-shell -p 'go_1_19'
```

I wonder how the default version selection mechanism works?