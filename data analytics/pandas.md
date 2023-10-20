find rows with blank fg_pct:

`df[df['fg_pct'].apply(lambda row: not isinstance(row, float))][["player", "fg_pct"]]`

select a few columns:

`df.head()[["player", "fg_pct"]]`

Replace all empty strings with zeroes:
- has an `inplace` argument to do it inplace, otherwise returns a copy

```python
>>> df["fg_pct"].replace("", 0)
0      0.405
1      0.630
2      0.514
3      0.667
4      0.385
       ...
401    0.333
402    0.458
403    0.667
404    0.667
405    0.600
Name: fg_pct, Length: 406, dtype: float64
```