https://github.com/dandavison/delta

`delta` gives git much nicer diff output in your console.

One great feature it supports is side-by-side diffs, which are great but don't work in narrow terminals; While that feature is still [not yet implemented by delta](https://github.com/dandavison/delta/issues/359), we can get its effect with a shell function in `~/.zshrc` or `~/.bashrc`:

```shell
# set side-by-side mode in delta only if the terminal is >= 120 lines. Assumes
# you don't have any other DELTA_FEATURES flags set.
# (https://github.com/dandavison/delta/issues/359)
export DELTA_FEATURES
function delta_sidebyside {
    if [[ "${COLUMNS}" -ge 120 ]]; then
        DELTA_FEATURES="side-by-side"
    else
        DELTA_FEATURES=""
    fi
}
# when the terminal resizes, WINCH gets called; check the width and determine 
# if side-by-side mode should be enabled
trap delta_sidebyside WINCH

# call delta_sidebyside at startup time to set the feature
delta_sidebyside
```