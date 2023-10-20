https://eli.thegreenplace.net/2023/rpc-based-plugins-in-go/

> 1.  Each plugin is a separate Go binary, built using some code shared with the main application.
> 2.  The main application loads plugins by running their binaries as sub-processes.
> 3.  The main application talks to plugins via RPC to access their functionality.

describes using https://github.com/hashicorp/go-plugin to develop a plugin system