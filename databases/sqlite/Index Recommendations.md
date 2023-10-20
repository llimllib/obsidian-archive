https://www.sqlite.org/cli.html#index_recommendations_sqlite_expert_

SQLite has the `.expert` command which can help you decide on what indexes to use

```sql
sqlite> CREATE TABLE x1(a, b, c);                  _-- Create table in database_ 
sqlite> .expert
sqlite> SELECT * FROM x1 WHERE a=? AND b>?;        _-- Analyze this SELECT_ 
CREATE INDEX x1_idx_000123a7 ON x1(a, b);

0|0|0|SEARCH TABLE x1 USING INDEX x1_idx_000123a7 (a=? AND b>?)

sqlite> CREATE INDEX x1ab ON x1(a, b);             _-- Create the recommended index_ 
sqlite> .expert
sqlite> SELECT * FROM x1 WHERE a=? AND b>?;        _-- Re-analyze the same SELECT_ 
(no new indexes)

0|0|0|SEARCH TABLE x1 USING INDEX x1ab (a=? AND b>?)
```

