---
created: 2026-06-24T12:57:42.693Z
updated: 2026-07-07T17:32:45.484Z
---
https://kolistat.com/blog/the-stats-duck-v0-6-0/

Announcement of a really neat duckdb extension called `the-stats-duck` ([KoliStat/the-stats-duck](https://github.com/KoliStat/the-stats-duck/)) which puts statistical functions inside duckDB.

It then goes on to add some visualization in duckdb sql, by serializing out to [[vega-lite]] format, á la [[ggsql]] (which the author calls out on [news.yc](https://kolistat.com/blog/the-stats-duck-v0-6-0/) as a direct inspiration)

My favorite bit is the function `meta()` as a _table-valued_ function, allowing you to select from it:

```sql
SELECT
  column_name, kind, n_missing , n_distinct, mean, median, stddev, top
FROM meta('penguins');
```

I don't use `R`, but I think that's basically the same as its `summary()` function.

It also builds in LOESS regression and embeds an R-like specification language for it:

```sql
SELECT *
FROM lm_summary(
  'penguins'
  , formula := 'body_mass_g ~ flipper_length_mm + bill_length_mm'
);
```

Also, neat job building the demo into WASM and serving it as part of the page, strong work.