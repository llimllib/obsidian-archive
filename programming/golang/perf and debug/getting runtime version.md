To get the git version number embedded in a go binary, use this function:

```go
func GetRuntimeVersion() string {
	if bi, ok := debug.ReadBuildInfo(); !ok {
		fmt.Println("Unable to get build info")
	} else {
		for i := range bi.Settings {
			if bi.Settings[i].Key == "vcs.revision" {
				return bi.Settings[i].Value
			}
		}
	}
	return ""
}
```

There are other useful values in there too. The full list from a random build right now:

```
&debug.BuildInfo{
  GoVersion:"go1.18",
  Path:"github.com/adhocteam/crosstree/cmd",
  Main:debug.Module{Path:"github.com/adhocteam/crosstree",
  Version:"(devel)",
  Sum:"",
}
-compiler: gc
CGO_ENABLED: 1
CGO_CFLAGS:
CGO_CPPFLAGS:
CGO_CXXFLAGS:
CGO_LDFLAGS:
GOARCH: arm64
GOOS: darwin
vcs: git
vcs.revision: 76abcbf15157346bdb1c341724da212d6694ee56
vcs.time: 2022-07-05T21:34:22Z
vcs.modified: true
```
