---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/ellie/atuin

> Atuin replaces your existing shell history with a SQLite database, and records additional context for your commands. Additionally, it provides optional and _fully encrypted_ synchronisation of your history between machines, via an Atuin server.

I'm going to try it out, because I _really_ want my history in a database instead of the janky history file.

Installs https://github.com/rcaloras/bash-preexec

`atuin import bash` imported my bash history

```
$ atuin stats all
+---------------------+----------+
| Statistic           | Value    |
+---------------------+----------+
| Most used command   | git pull |
+---------------------+----------+
| Commands ran        |     8449 |
+---------------------+----------+
| Unique commands ran |     5560 |
+---------------------+----------+
```

looks about right.

Stores the db at `./.local/share/atuin/history.db`, and indeed it's a simple queryable sqlite database. The config file at `~/.config/atuin/config.toml` will let you change the path as well as [some other stuff](https://github.com/ellie/atuin/blob/main/docs/config.md), but I'm just gonna leave it at the default state for now.

Would like to use litestream to back it up to s3.

Is it still echoing to `~/.bash_history`? Yup:

```
$ tail ~/.bash_history
#1650679383
git co master
#1650679389
git branch -D exclude-take-3
#1650679393
git pull
#1650985607
ls testing

$ sqlite3 ./.local/share/atuin/history.db 'select command from history order by timestamp desc limit 5;'
sqlite3 ./.local/share/atuin/history.db 'select command from history order by timestamp desc limit 5;'
sqlite3 ./.local/share/atuin/history.db -c 'select command from history order by timestamp desc limit 5;'
tail ~/.bash_history
ls testing
tail ~/.bash_history
```

Has [search subcommand](https://github.com/ellie/atuin/blob/main/docs/search.md) if you don't want to just query the db

[this person](https://github.com/pitr/config_files) has set up litestream replication for their atuin db, maybe I can crib from them.

replaces my fzf ctrl-r binding with something a bunch worse

Seems like you need to prepend any query with `*`; `atuin search jq` shows no results but `atuin search '*jq'` yields what I'd expect.

ah ha! go to `~/.config/atuin/config.toml` and set `search_mode` to `fuzzy`. [docs here](https://github.com/ellie/atuin/blob/b22929222f7328422e0eb9e4a5dfe538f91b37b8/docs/config.md):

```toml
## which search mode to use
## possible values: prefix, fulltext, fuzzy
search_mode = "fuzzy"
```

To merge history from one machine into another:

- copy the database file from `~/.local/share/atuin/history.db` to the remote machine
- open sqlite on the machine you want to merge the files on with `sqlite3 ~/.local/share/atuin/history.db`
- attach the remote file and insert it into the local history like so:
```
$ sqlite3 ~/.local/share/atuin/history.db
SQLite version 3.39.5 2022-10-14 20:58:05
Enter ".help" for usage hints.
sqlite> attach '/path/to/remote/history.db' as remotehist;
sqlite> begin;
sqlite> insert into history select * from remotehist.history;
sqlite> commit;
sqlite> detach remotehist;
```