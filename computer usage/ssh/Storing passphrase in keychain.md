```console
$ ssh-add --apple-use-keychain ~/.ssh/billmill.org.key
Enter passphrase for /Users/llimllib/.ssh/billmill.org.key:
Identity added: /Users/llimllib/.ssh/billmill.org.key (key for billmill.org)
```

that's it! now you can just use that key and ssh will grab the passphrase from keychain.

From [here](https://apple.stackexchange.com/a/250572/303719), with a useful caveat:

> (If this fails, make sure you are using Apple's version of `/usr/bin/ssh-add` and not something installed with brew etc.; check with `which ssh-add`)

I missed step two, which is to add it to the ssh config file `~/.ssh/config`:

```
 Host *
   UseKeychain yes
   AddKeysToAgent yes
   IdentityFile <keyfile>
   ...any amount of IdentityFiles you want ot use keychain for...
```

