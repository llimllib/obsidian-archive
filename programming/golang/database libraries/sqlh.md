---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/nofeaturesonlybugs/sqlh

> Powerful struct scanning for Go's database/sql and other compatible interfaces.

> `sqlh` is easy to use because it lives very close to `database/sql`. The primary goal of `sqlh` is to work with and facilitate using `database/sql` without replacing or hijacking it. When using `sqlh` you manage your `*sql.DB` or create `*sql.Tx` as you normally would and pass those as arguments to functions in `sqlh` when scanning or persisting models; `sqlh` then works within the confines of what you gave it.

> When accepting arguments that work directly with the database (`*sql.DB` or `*sql.Tx`) `sqlh` accepts them as interfaces. This means `sqlh` may work with other database packages that define their own types as long as they kept a method set similar to `database/sql`.