---
created: 2026-04-17T13:23:40.062Z
updated: 2026-04-17T13:23:40.062Z
---
> We call an application _data intensive_ if data management is one of the primary challenges in developing the application. While in _compute-intensive_ systems the challenge is parallelizing a very large computation, in data-intesnive applications we usually worry more about things like storing and processing large data volumes

---

The difference in use between backend engineers (who modify data & generally look at one user at a time) and business analysts/data scientists has led to a split between _operational systems_ and _analytical systems_ that are often kept separate.

---

**point query**: a query that looks up a small number of records based on a _key_
**OLTP**: Online Transaction Processing - a system that inserts, updates or deletes records generally based on a key
**OLAP**: Online Analytical Processing - a system that generally scans a huge number of records to calculate aggregate statistics rather than returning individual records to the user

They differentiate ClickHouse etc (Pinot, Druid? never heard of them) as **product analytics** or **real-time analytics** which are designed for analytical workloads, but serve user-facing products

---

Data from OLTP systems is often spread across the enterprise, and BAs do not want to have to query across potentially dozens of systems. A **data warehouse** contains data extracted from many OLTP systems in a company. (They go on to say that it can come from many other sources as well, which is more accurate imo)

A data warehouse often uses relational tables, which is well suited to what BAs want, but less well suited to data scientists' desires, training ML models and using NLP or computer vision.

(They say that feature engineering is particularly difficult to express using SQL? I'd like to understand what they mean by that more here. `[citation needed]`)

a **data lake** is a centralized data repository that holds a copy of any data that might be useful for analysis. The difference from a data warehouse is that a data lake simply contains files, without imposing any particular file format. (So, s3 is a data lake? Seems like a kinda useless definition imo)

---
>  the term **cloud native** is used to describe an architecture that is designed to take advantage of cloud services

This is an extremely fuzzy definition to me. They say that Postgres and ClickHouse are self-hosted systems that are not cloud native, but that Aurora and Snowflake are cloud-native, and I think you'd be hard-pressed to really apply the definition above to make that distinction clear.

The things that distinguish them to me are:

- usually specialized to the operating environment of a particular cloud service provider
- usually not available as open source
- usually not available to run on a general-purpose computer, or available but in severely degraded form

To me, if we want to split the mysqls and postgreses of the world from the aurorae and BigQueries, it's about how _specialized_ they are to cloud service providers' computers as opposed to general-purpose computation

> The key idea of cloud native services is not only to use the computing resources managed by your operating system, but also to build upon the lower-level cloud services to create higher-level services

yeah that's closer for me