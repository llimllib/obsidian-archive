---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/BurntSushi/xsv

> A fast CSV command line toolkit written in Rust.

### Available commands

-   **cat** - Concatenate CSV files by row or by column.
-   **count** - Count the rows in a CSV file. (Instantaneous with an index.)
-   **fixlengths** - Force a CSV file to have same-length records by either padding or truncating them.
-   **flatten** - A flattened view of CSV records. Useful for viewing one record at a time. e.g., `xsv slice -i 5 data.csv | xsv flatten`.
-   **fmt** - Reformat CSV data with different delimiters, record terminators or quoting rules. (Supports ASCII delimited data.)
-   **frequency** - Build frequency tables of each column in CSV data. (Uses parallelism to go faster if an index is present.)
-   **headers** - Show the headers of CSV data. Or show the intersection of all headers between many CSV files.
-   **index** - Create an index for a CSV file. This is very quick and provides constant time indexing into the CSV file.
-   **input** - Read CSV data with exotic quoting/escaping rules.
-   **join** - Inner, outer and cross joins. Uses a simple hash index to make it fast.
-   **partition** - Partition CSV data based on a column value.
-   **sample** - Randomly draw rows from CSV data using reservoir sampling (i.e., use memory proportional to the size of the sample).
-   **reverse** - Reverse order of rows in CSV data.
-   **search** - Run a regex over CSV data. Applies the regex to each field individually and shows only matching rows.
-   **select** - Select or re-order columns from CSV data.
-   **slice** - Slice rows from any part of a CSV file. When an index is present, this only has to parse the rows in the slice (instead of all rows leading up to the start of the slice).
-   **sort** - Sort CSV data.
-   **split** - Split one CSV file into many CSV files of N chunks.
-   **stats** - Show basic types and statistics of each column in the CSV file. (i.e., mean, standard deviation, median, range, etc.)
-   **table** - Show aligned output of any CSV data using [elastic tabstops](https://github.com/BurntSushi/tabwriter).