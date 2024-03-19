https://buck2.build/
https://buck2.build/docs/getting_started/

A build system by (among others) Neil Mitchell, one of the authors of [[Build systems á la carte]], one of my favorite papers.

I read the manual, and I'll be honest with you that I have no idea at all what is going on here, or how somebody could learn to use this system.

For example, let's say I wanted to use it to bundle my javascript, ok there's a function `js_bundle`, great! Let's look at [the docs](https://buck2.build/docs/api/rules/#js_bundle)!

Umm, what? If I ran that rule I have no idea at all what would actually happen on my computer, which is here on earth, not in outer space where this command resides.

It also appears to have some relation to bazel - you put rule files in starlark code with the extension `.bzl` - that I don't understand. It makes it impossible to do a github code search to find examples that use `buck2` rather than `bazel` - there appear to be far more of the latter than the former.