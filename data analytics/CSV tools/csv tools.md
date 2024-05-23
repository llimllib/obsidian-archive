---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
## CSV querying libraries:

- [[miller]] - slow but thorough and multi-format (json, csv, tsv)
- [[xsv]] - faster, but no release since 2018. Author seems busy with other stuff (not complaining)
	- 2023 update: unfortunately still no releases, seems completely abandoned
- [[zsv]] - very fast csv tools, [[programming/C/C|C]], never used it
- [[qsv]] - very fast csv tools, [[rust]], never used it. Will turn json to csv (not sure how). Fork of xsv
- [[csvkit]] - slow, but the most thorough csv tools I know of
- [q](http://harelba.github.io/q/) - run sql directly on CSV or TSV files
- [csvtk](https://bioinf.shenwei.me/csvtk/) golang tools, looks similar to qsv. Has plot tools, which is neat

Or you could [load and query your CSV through slqite](https://til.simonwillison.net/sqlite/one-line-csv-operations)

## CSV terminal output
[tv](https://github.com/alexhallam/tv) - tidy viewer:

> Tidy Viewer (tv) is a cross-platform csv pretty printer that uses column styling to maximize viewer enjoyment.

`brew install tidy-viewer`

[visidata](https://www.visidata.org/):

> VisiData is an interactive multitool for tabular data. It combines the clarity of a spreadsheet, the efficiency of the terminal, and the power of Python, into a lightweight utility which can handle millions of rows with ease.

has several of the functionalities of the querying libs, but also is a UI and can even show graphs in the terminal