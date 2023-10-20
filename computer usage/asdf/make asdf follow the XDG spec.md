To make `asdf` roughly follow the XDG spec:

- (I'm assuming that you want to use default XDG dirs, replace `~/.local/share` with `XDG_DATA` and `~/.local/config` with `XDG_CONFIG` as necessary if you don't)
- install it to `~/.local/share/asdf`:
	- `git clone https://github.com/asdf-vm/asdf.git ~/.local/share/asdf --branch v0.11.3`
- set a whole bunch of environment variables. Here's the section from my `~/.bashrc`:

```bash
if [[ -d $HOME/.local/share/asdf ]]; then
    # I really wish asdf supported XDG_CONFIG:
    # https://github.com/asdf-vm/asdf/issues/687
    #
    # so let's set a bunch of variables that let us pretend it does
    export ASDF_DIR="$HOME/.local/share/asdf"
    export ASDF_DATA_DIR="$HOME/.local/share/asdf"

    . "$ASDF_DIR/asdf.sh"
    . "$ASDF_DIR/completions/asdf.bash"

    # https://asdf-vm.com/manage/configuration.html#asdfrc
    export ASDF_CONFIG_FILE="$HOME/.config/asdf/asdfrc"

    # https://github.com/asdf-vm/asdf-nodejs#default-npm-packages
    export ASDF_NPM_DEFAULT_PACKAGES_FILE="$HOME/.config/asdf/default-npm-packages"

    # https://github.com/asdf-community/asdf-python#default-python-packages
    export ASDF_PYTHON_DEFAULT_PACKAGES_FILE="$HOME/.config/asdf/default-python-packages"
fi
```

Once you have those variables set, you should have asdf config in `~/.config/asdf` and asdf binaries and package installs in `~/.local/share/asdf`.

If you already have `asdf` installed to the default location of `~/.asdf`, you can move that directory into `~/.config/asdf` and run `asdf reshim`.
- unfortunately the python builds embed the directory for the location of shared modules, I had to blow away and re-install python to move it successfully

[this issue](https://github.com/asdf-vm/asdf/issues/687) tracks asdf support of the XDG spec