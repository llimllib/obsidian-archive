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

