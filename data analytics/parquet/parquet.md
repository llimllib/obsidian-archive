---
updated: '2023-11-06T16:15:37Z'
created: '2023-10-20T13:54:09Z'
---
https://parquet.apache.org/

> Apache Parquet is an open source, column-oriented data file format designed for efficient data storage and retrieval. It provides efficient data compression and encoding schemes with enhanced performance to handle complex data in bulk. Parquet is available in multiple languages including Java, C++, Python, etc...

A lot of [[duckdb]] seems to be oriented around using parquet files. The command line tools for manipulating them don't seem to be great so far.

The best way I've found to head a parquet file so far is to use pandas:

```
python -c "import pandas; df=pandas.read_parquet('data/playerstats.parquet'); print(df.tail(10).to_csv())"
```

I print it as csv because then I can display it nicely with [[tv]]:

```
python -c "import pandas; df=pandas.read_parquet('data/playerstats.parquet'); print(df.tail(40).to_csv())" | tv -ea | bat
```

piping it to [[bat]] makes it so that you can scroll through all the columns; if you don't do that `tv` will tell you what columns it isn't displaying, but it won't show them.

Neat, if you use [nushell](https://github.com/nushell/nushell), it's just:

```
/Users/llimllib/code/nbastats〉open-df playerstats.parquet
╭──────┬───────────┬─────────────┬──────────┬────────────┬─────╮
│    # │ PLAYER_ID │ PLAYER_NAME │ NICKNAME │  TEAM_ID   │ ... │
│      │           │             │          │            │     │
├──────┼───────────┼─────────────┼──────────┼────────────┼─────┤
│    0 │    201985 │ AJ Price    │ AJ       │ 1610612754 │ ... │
│    1 │    201166 │ Aaron       │ Aaron    │ 1610612745 │ ... │
│      │           │ Brooks      │          │            │     │
│    2 │    201189 │ Aaron Gray  │ Aaron    │ 1610612740 │ ... │
```

---

parquet includes a CLI in its project (`brew install parquet-cli`). It's a java program though, so naturally it's a terrible CLI citizen. It also appears to be completely undocumented on the [parquet site](https://parquet.apache.org/docs/) and comes with no man page.

anyway, `parquet cat -10 <file>` will print the first 10 rows, and `-c` will select columns:

```
$ parquet cat playerstats.parquet -n 10 -c player_name,team_abbreviation
{"player_name": "AJ Price", "team_abbreviation": "MIN"}
{"player_name": "Aaron Brooks", "team_abbreviation": "DEN"}
{"player_name": "Aaron Gray", "team_abbreviation": "SAC"}
{"player_name": "Adonis Thomas", "team_abbreviation": "PHI"}
{"player_name": "Al Harrington", "team_abbreviation": "WAS"}
{"player_name": "Al Horford", "team_abbreviation": "ATL"}
{"player_name": "Al Jefferson", "team_abbreviation": "CHA"}
{"player_name": "Al-Farouq Aminu", "team_abbreviation": "NOP"}
{"player_name": "Alan Anderson", "team_abbreviation": "BKN"}
{"player_name": "Alec Burks", "team_abbreviation": "UTA"}
```

Note that normal unix arguments like `-n10` instead of `-n` will not work.

`parquet help cat` will print the documentation for that subcommand, but `parquet cat --help` will try to open the `--help` file.

