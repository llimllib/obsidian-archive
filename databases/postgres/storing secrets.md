---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://supabase.com/blog/supabase-vault
https://github.com/supabase/vault

> Many applications have sensitive data that must have additional storage protection relative to other data. For example, your application may access external services with an "API Key". This key is issued to you by that specific external service provider, and you must keep it safe from being stolen or leaked. If someone got their hands on your payment processor key, for example, they may be able to use it to send money or digital assets out of your account to someone else. Wherever this key is stored, it would make sense to store it in an encrypted form.

> Supabase provides a table called `vault.secrets` that can be used to store sensitive information like API keys. These secrets will be stored in an encrypted format on disk and in any database dumps. Decrypting this table is done through a special "view" object called `pgsodium_masks.secrets` that uses an encryption key that is itself not avaiable to SQL, but can be referred to by ID. Supabase manages these internal keys for you, so you can't leak them out of the database, you can only refer to them by their ids.

Built on top of [pgsodium](https://github.com/michelp/pgsodium), which is itself built on top of [[libsodium]]