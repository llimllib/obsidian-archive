---
updated: 2025-05-18T11:50:37Z
created: 2023-10-20T13:54:09Z
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

----

https://github.com/manojkarthick/pqrs

PQRS is a better CLI than the `parquet-cli` one

```
$ pqrs head four_factors.parquet
{gameId: "0022200971", team: "BOS", 2pt_oScPoss: 26, 2pt_oPoss: 44.352, 2pt_oPtsProd: 52, 2pt_oNetPts: 1.1726, 3pt_oScPoss: 16, 3pt_oPoss: 40.94, 3pt_oPtsProd: 48, 3pt_oNetPts: 1.9789, freethrow_oScPoss: 4.5, freethrow_oPoss: 7.76, freethrow_oPtsProd: 14.0, freethrow_oNetPts: 5.107, rebound_oScPoss: 0, rebound_oPoss: -1.052E0, rebound_oPtsProd: 0, rebound_oNetPts: 1.4554, turnover_oScPoss: 0, turnover_oPoss: 14.0, turnover_oPtsProd: 0, turnover_oNetPts: -1.6044E1}
{gameId: "0022200971", team: "CLE", 2pt_oScPoss: 31, 2pt_oPoss: 52.22, 2pt_oPtsProd: 62, 2pt_oNetPts: 2.1559, 3pt_oScPoss: 12, 3pt_oPoss: 28.952, 3pt_oPtsProd: 36, 3pt_oNetPts: 2.821, freethrow_oScPoss: 7.5, freethrow_oPoss: 9.76, freethrow_oPtsProd: 20.0, freethrow_oNetPts: 8.815, rebound_oScPoss: 0, rebound_oPoss: -9.32E-1, rebound_oPtsProd: 0, rebound_oNetPts: 1.0681, turnover_oScPoss: 0, turnover_oPoss: 15.0, turnover_oPtsProd: 0, turnover_oNetPts: -1.719E1}
{gameId: "0022200972", team: "IND", 2pt_oScPoss: 38, 2pt_oPoss: 48.239, 2pt_oPtsProd: 76, 2pt_oNetPts: 20.7181, 3pt_oScPoss: 15, 3pt_oPoss: 32.12, 3pt_oPtsProd: 45, 3pt_oNetPts: 10.2327, freethrow_oScPoss: 8.5, freethrow_oPoss: 11.4, freethrow_oPtsProd: 22.0, freethrow_oNetPts: 8.9356, rebound_oScPoss: 0, rebound_oPoss: 2.241, rebound_oPtsProd: 0, rebound_oNetPts: -2.3184E0, turnover_oScPoss: 0, turnover_oPoss: 9.0, turnover_oPtsProd: 0, turnover_oNetPts: -1.0314E1}
{gameId: "0022200972", team: "PHI", 2pt_oScPoss: 32, 2pt_oPoss: 42.939, 2pt_oPtsProd: 64, 2pt_oNetPts: 15.9379, 3pt_oScPoss: 16, 3pt_oPoss: 29.908, 3pt_oPtsProd: 48, 3pt_oNetPts: 13.7254, freethrow_oScPoss: 14.6667, freethrow_oPoss: 15.88, freethrow_oPtsProd: 35.0, freethrow_oNetPts: 16.8015, rebound_oScPoss: 0, rebound_oPoss: 1.273, rebound_oPtsProd: 0, rebound_oNetPts: -1.4589E0, turnover_oScPoss: 0, turnover_oPoss: 12.0, turnover_oPtsProd: 0, turnover_oNetPts: -1.3752E1}
{gameId: "0022200974", team: "ATL", 2pt_oScPoss: 42, 2pt_oPoss: 56.455, 2pt_oPtsProd: 84, 2pt_oNetPts: 19.3026, 3pt_oScPoss: 9, 3pt_oPoss: 24.556, 3pt_oPtsProd: 27, 3pt_oNetPts: 0.901, freethrow_oScPoss: 7.6667, freethrow_oPoss: 9.52, freethrow_oPtsProd: 17.0, freethrow_oNetPts: 6.0901, rebound_oScPoss: 0, rebound_oPoss: -3.531E0, rebound_oPtsProd: 0, rebound_oNetPts: 4.2964, turnover_oScPoss: 0, turnover_oPoss: 11.0, turnover_oPtsProd: 0, turnover_oNetPts: -1.2606E1}

$ pqrs head four_factors.parquet --csv
gameId,team,2pt_oScPoss,2pt_oPoss,2pt_oPtsProd,2pt_oNetPts,3pt_oScPoss,3pt_oPoss,3pt_oPtsProd,3pt_oNetPts,freethrow_oScPoss,freethrow_oPoss,freethrow_oPtsProd,freethrow_oNetPts,rebound_oScPoss,rebound_oPoss,rebound_oPtsProd,rebound_oNetPts,turnover_oScPoss,turnover_oPoss,turnover_oPtsProd,turnover_oNetPts
0022200971,BOS,26,44.352,52,1.1726,16,40.94,48,1.9789,4.5,7.76,14.0,5.107,0,-1.052,0,1.4554,0,14.0,0,-16.044
0022200971,CLE,31,52.22,62,2.1559,12,28.952,36,2.821,7.5,9.76,20.0,8.815,0,-0.932,0,1.0681,0,15.0,0,-17.19
0022200972,IND,38,48.239,76,20.7181,15,32.12,45,10.2327,8.5,11.4,22.0,8.9356,0,2.241,0,-2.3184,0,9.0,0,-10.314
0022200972,PHI,32,42.939,64,15.9379,16,29.908,48,13.7254,14.6667,15.88,35.0,16.8015,0,1.273,0,-1.4589,0,12.0,0,-13.752
0022200974,ATL,42,56.455,84,19.3026,9,24.556,27,0.901,7.6667,9.52,17.0,6.0901,0,-3.531,0,4.2964,0,11.0,0,-12.606
```