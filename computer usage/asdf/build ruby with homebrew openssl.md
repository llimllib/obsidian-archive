```
RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl)" \
    asdf install ruby latest
```

If you don't do this, asdf will want to to download and build its own copy of openssl, which can take a while. 

(On the upside, you won't be depending on homebrew to have the right version and not to clean it up someday because it doesn't know about this dependency, but you can't win 'em all I suppose)