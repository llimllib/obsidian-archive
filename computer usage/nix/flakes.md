To enable:

```
mkdir ~/.config/nix
echo 'experimental-features = nix-command flakes' >> ~/.config/nix/nix.conf
```

The [blog article I'm reading](https://ghedam.at/a-tour-of-nix-flakes) has [a link to the NixOS wiki page](https://nixos.wiki/wiki/Flakes)

I'm in a directory with a flake, and now:

```
$ nix flake show
git+file:///Users/llimllib/somedir/main?ref=refs%2fheads%2fmain&rev=2245bf45a150fce882aa4070b6929b4992c2d0fc
└───devShell
    ├───aarch64-darwin: development environment 'nix-shell'
    ├───aarch64-linux: development environment 'nix-shell'
    ├───i686-linux: development environment 'nix-shell'
    ├───x86_64-darwin: development environment 'nix-shell'
    └───x86_64-linux: development environment 'nix-shell'
```

I don't really understand what this is telling me? but ok