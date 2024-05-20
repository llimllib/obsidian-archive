---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
[pola.rs](https://www.pola.rs/) looks super neat:

> Lightning-fast DataFrame library for Rust and Python

> Polars is written in Rust, uncompromising in its choices to provide a feature-complete DataFrame API to the Rust ecosystem. Use it as a DataFrame library or as query engine backend for your data models.

> Polars is built upon the [ safe Arrow2 implementation](https://github.com/jorgecarleitao/arrow2) of the [ Apache Arrow specification](https://arrow.apache.org/docs/format/Columnar.html), enabling efficient resource use and processing performance. By doing so it also integrates seamlessly with other tools in the Arrow ecosystem.

They are [working on a webassembly version](https://github.com/pola-rs/polars/issues/83), but there's nothing released yet. Would love to use this for [[NBA Stats]]

[here](https://github.com/alecstein/dolt_datascience/blob/master/hospitals_v3/2022-05-06-prices-compared-with-medicare.ipynb) is an ipython notebook demonstrating usage of polars with a neat medicare data set. Shows off a handy feature of polars compared to pandas that it can filter the data on read, rather than having to load it all into memory first. Also uses [[Altair]] for visualization

----

https://kevinheavey.github.io/modern-polars/

> This is a side-by-side comparison of the [Polars](https://www.pola.rs/) and [Pandas](https://pandas.pydata.org/) dataframe libraries, based on [Modern Pandas](https://tomaugspurger.github.io/posts/modern-8-scaling/) by Tom Augsburger.

> (In case you haven’t heard, Polars is a very fast and elegant dataframe libary that does the same kinds of things Pandas does.)

> The bulk of this book is structured examples of idiomatic Polars and Pandas code, with commentary on the API and performance of both.

> For the most part, I argue that Polars is “better” than Pandas, though I do try and make it clear when Polars is lacking a Pandas feature or is otherwise disappointing.