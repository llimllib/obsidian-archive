https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md

> When I first started writing SQLGlot in early 2021, my goal was just to translate SQL queries from SparkSQL to Presto and vice versa. However, over the last year and a half, I've ended up with a full-fledged SQL engine. SQLGlot can now parse and transpile between [18 SQL dialects](https://github.com/tobymao/sqlglot/blob/main/sqlglot/dialects/__init__.py) and can execute all 24 [TPC-H](https://www.tpc.org/tpch/) SQL queries. The parser and engine are all written from scratch using Python.

> This post will cover [why](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#why) I went through the effort of creating a Python SQL engine and [how](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#how) a simple query goes from a string to actually transforming data. The following steps are briefly summarized:

> -   [Tokenizing](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#tokenizing)
> -   [Parsing](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#parsing)
> -   [Optimizing](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#optimizing)
> -   [Planning](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#planning)
> -   [Executing](https://github.com/tobymao/sqlglot/blob/main/posts/python_sql_engine.md#executing)


[[compilers]]