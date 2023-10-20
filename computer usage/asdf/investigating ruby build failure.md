
To build ruby with the system openssl, instead of downloading and building its own copy:

```shell
RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@1.1)" \
  asdf install ruby latest
```

To find out why my build is failing, I added `set -x` to `~/.asdf/plugins/ruby/bin/install`:

```
$ git diff

diff --git bin/install bin/install
index b3f5cea..2aa70f9 100755
--- bin/install
+++ bin/install
@@ -2,6 +2,10 @@

 set -euo pipefail

+# added by llimllib for debugging
+set -x
+# DELETEME
+
 # shellcheck source=/dev/null
 source "$(dirname "$0")/../lib/utils.sh"

```

This logged the ruby-build invocation, but didn't apply to ruby-build itself. But it did show me that it ran `.asdf/plugins/ruby/ruby-build/bin/ruby-build`, so let's try the same trick on that

`~/.asdf/plugins/ruby/ruby-build/bin/ruby-build 3.1.2 ~/.asdf/installs/ruby/3.1.2`

ruby-build sources `~/.asdf/plugins/ruby/ruby-build/share/ruby-build/3.1.2`, which has two commands:

```
install_package "openssl-3.0.5" "https://www.openssl.org/source/openssl-3.0.5.tar.gz#aa7d8d9bef71ad6525c55ba11e5f4397889ce49c2c9349dcea6d3e4f0b024a7a" openssl --if needs_openssl_102_300
install_package "ruby-3.1.2" "https://cache.ruby-lang.org/pub/ruby/3.1/ruby-3.1.2.tar.gz#61843112389f02b735428b53bb64cf988ad9fb81858b8248e22e57336f24a83e" ldflags_dirs enable_shared standard verify_openssl
```

the first doesn't execute because I gave it a proper openssl already. The second ends up calling:

```
build_package ruby-3.1.2 ldflags_dirs enable_shared standard verify_openssl
# which then calls
build_package_ldflags_dirs ruby-3.1.2
```

Then the trail goes cold after `set - $LDFLAGS` - I have no idea what that is supposed to be doing! I added a `set -x` after it to see if that changes anything?

That ultimately calls this `make` command that is failing:

```
++ make -j 8
	BASERUBY = /usr/bin/ruby --disable=gems
	CC = clang
	LD = clang
	LDSHARED = clang -dynamiclib
	CFLAGS = -fdeclspec -O3 -fno-fast-math -ggdb3 -Wall -Wextra -Wdeprecated-declarations -Wdivision-by-zero -Wimplicit-function-declaration -Wimplicit-int -Wmisleading-indentation -Wpointer-arith -Wshorten-64-to-32 -Wwrite-strings -Wold-style-definition -Wmissing-noreturn -Wno-cast-function-type -Wno-constant-logical-operand -Wno-long-long -Wno-missing-field-initializers -Wno-overlength-strings -Wno-parentheses-equality -Wno-self-assign -Wno-tautological-compare -Wno-unused-parameter -Wno-unused-value -Wunused-variable -Wextra-tokens -Wundef -std=gnu99  -fno-common -pipe 
	XCFLAGS = -D_FORTIFY_SOURCE=2 -fstack-protector-strong -fno-strict-overflow -fvisibility=hidden -DRUBY_EXPORT -I. -I.ext/include/arm64-darwin21 -I./include -I. -I./enc/unicode/13.0.0
	CPPFLAGS = -I/Users/llimllib/.asdf/installs/ruby/3.1.2/include  -D_XOPEN_SOURCE -D_DARWIN_C_SOURCE -D_DARWIN_UNLIMITED_SELECT -D_REENTRANT   
	DLDFLAGS = -L/Users/llimllib/.asdf/installs/ruby/3.1.2/lib  -Wl,-multiply_defined,suppress -install_name /Users/llimllib/.asdf/installs/ruby/3.1.2/lib/libruby.3.1.dylib -compatibility_version 3.1 -current_version 3.1.2  -fstack-protector-strong -framework CoreFoundation  -fstack-protector-strong -framework CoreFoundation  
	SOLIBS = -lpthread -ldl -lobjc
	LANG = en_US.UTF-8
	LC_ALL = 
	LC_CTYPE = 
	MFLAGS = - --jobserver-fds=6,7 -j
```

oh man is it this stupid? `mkdir -p ~/.asdf/installs/ruby/3.1.2/{bin,lib,include}`

idea via [this comment](https://github.com/rbenv/ruby-build/issues/992#issuecomment-556120333)

alright if you do that before trying `asdf install` it doesn't work, because `asdf` then believes it already has version 3.1.2, so I added it to the ruby build script - now I get a new failure at least.

```shell
--- ruby-build/bin/ruby-build	2022-10-18 11:14:28.000000000 -0400
+++ ruby-build/bin/ruby-build.bak	2022-10-18 11:19:11.000000000 -0400
@@ -582,12 +582,6 @@
       use_homebrew_gmp || true
   fi

-  # llimllib
-  echo "------------->"
-  set -x
-  # DELETEME
-  mkdir -p ~/.asdf/installs/ruby/3.1.2/{bin,lib,include}
-
   ( if [ "${CFLAGS+defined}" ] || [ "${!PACKAGE_CFLAGS+defined}" ]; then
       export CFLAGS="$CFLAGS ${!PACKAGE_CFLAGS}"
     fi
```

now we have:

```
 858   │ compiling addr2line.c
 859   │ compiling dmyenc.c
 860   │ make: ./config.status: Permission denied
 861   │ make: *** [ruby-runner.h] Error 1
 862   │ make: *** Waiting for unfinished jobs....
 ```
ok to find those `compiling` messages, I had to find `common.mk`, which seems to have some more makefile stuff in it. _That_ file indicates that there is a `V` option, which if set to 1, will cause it to log verbosely:

```
# V=0 quiet, V=1 verbose.  other values don't work.
V = 0
```

To set that, I just jimmied the make command to add V=1 because I didn't figure out how to add it to the argument array properly, and who cares:

```
  # llimllib: remove V=1 when done debugging
  { "$MAKE" "${!PACKAGE_MAKE_OPTS_ARRAY}" $MAKE_OPTS V=1 ${!PACKAGE_MAKE_OPTS}
```

ok, the miniruby command that failed now shows up!

```
./miniruby -I./lib -I. -I.ext/common  ./tool/generic_erb.rb -o builtin_binary.inc \
		./template/builtin_binary.inc.tmpl -- --cross=no
```

sadly, when I cd into the directory and run it myself, it succeeds:

```
$ ./miniruby -I./lib -I. -I.ext/common  ./tool/generic_erb.rb -o builtin_binary.inc \
                ./template/builtin_binary.inc.tmpl -- --cross=no
builtin_binary.inc updated
```

urgggg just going into the dir and doing `make install` works. Very frustrating!

ok, now asdf wrote over my version of ruby-build. So let's clone ruby-build, and work on it in its own dir:

```
$ RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@3)" bin/ruby-build 3.1.2 /tmp/wut
... omitted
compiling yjit.c
make: /opt/homebrew/bin/gmkdir: Permission denied
make: *** [coroutine/arm64/.time] Error 1
make: *** Waiting for unfinished jobs....
```

ok let's try adding V=1 again. Here's the patch I applied:

```
diff --git bin/ruby-build bin/ruby-build
index 517bc15..d45c4ba 100755
--- bin/ruby-build
+++ bin/ruby-build
@@ -568,6 +568,13 @@ build_package_standard_build() {
     MAKE_OPTS="-j $(num_cpu_cores)"
   fi

+  if [ "${VERBOSE+defined}" ]; then
+    echo "adding V=1"
+    MAKE_OPTS="V=1"
+  else
+    exit 1
+  fi
+
```

f*$&, it worked this time! cmon man I need you to fail here.

And now... it just succeeds with asdf, no changes required. That sucks.