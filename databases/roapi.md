https://github.com/roapi/roapi

> ROAPI automatically spins up read-only APIs for static datasets without requiring you to write a single line of code. It builds on top of [Apache Arrow](https://github.com/apache/arrow) and [Datafusion](https://github.com/apache/arrow-datafusion). The core of its design can be boiled down to the following:

So the idea here, if I'm following is: 

- you have a dataset, and you want to spin up an API server for it
	- but you don't want to write it by hand
- you tell roapi where your data set is
	- google sheet
	- airtable
	- file on your fs
	- s3/gcs/azure
	- postgres/mysql/sqlite
- it automatically creates an API server that accepts queries in
	- sql
	- graphql
	- rest
- and outputs them in a format
	- arrow
	- json
	- messagepack
	- parquet

cf [[tuql]], which does a small part of this