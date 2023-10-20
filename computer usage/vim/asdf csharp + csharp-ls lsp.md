To get csharp installed from asdf:

```bash
asdf plugin-add dotnet-core https://github.com/emersonsoares/asdf-dotnet-core.git
asdf install dotnet-core latest 
```

This gets you dotnet installed in your asdf folder, but to get dotnet to recognize this non-standard folder is a bit of a goat rodeo. First, you need to [source the appropriate shell file](https://github.com/hensou/asdf-dotnet/blob/78b81e4b5ea9c51fad7914ea6a593c63f28a4d11/README.md#updating-dotnet_root-and-msbuildsdkspath) which adds the `DOTNET_ROOT` environment variable pointing to the correct installation folder.

Then, for [csharp-ls](https://github.com/razzmatazz/csharp-language-server/) to work, you need to make sure that the _actual_ dotnet binary, not the asdf shim, is found first on your path; I solved this by adding this to my `.envrc` in the C# project I was working on: `export PATH=$DOTNET_ROOT:$PATH`; this ensures that `dotnet`-the-binary is found before dotnet-the-asdf-shim.

(The reason for this is [this bug](https://github.com/microsoft/MSBuildLocator/issues/210) in Microsoft's code. It's ridiculous that they claim dotnet ought to be usable on non-windows systems, IMO. Many thanks to `hochata` on github for [posting the solution](https://github.com/razzmatazz/csharp-language-server/issues/82#issuecomment-1502608323))

Then, I added the csharp-ls config to my lsp config:

```lua
lsp.csharp_ls.setup({ on_attach = on_attach, capabilities = capabilities })
```

and finally I was off and running!