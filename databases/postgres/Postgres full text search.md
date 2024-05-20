---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
[[Postgres]] has two types of text search, full text and trigram

## full text search

documented here: https://www.postgresql.org/docs/14/textsearch.html

## trigram search

Useful article, "optimizing postgres]trigram search": https://alexklibisz.com/2022/02/18/optimizing-postgres-trigram-search.html

> why not full-text search?
> From some experimenting with Full Text Search, I’ve found the API focuses more narrowly on natural language text (i.e., words, spaces, punctuation), than on general-purpose text (i.e., natural language text _and_ product SKUs _and_ email addresses, …)

## why not to use?

gitlab hit scaling limits with both trigram search and full-text search, and documented their journey from postgres to elasticsearch:

> GitLab’s evolution from Postgres Trigrams to Elasticsearch [Fast Search Using PostgreSQL Trigram Text Indexes (March 2016)](https://about.gitlab.com/blog/2016/03/18/fast-search-using-postgresql-trigram-indexes/), [Lessons from our journey to enable global code search with Elasticsearch on GitLab.com (March 2019)](https://about.gitlab.com/blog/2019/03/20/enabling-global-search-elasticsearch-gitlab-com/), [Update: The challenge of enabling Elasticsearch on GitLab.com (July 2019)](https://about.gitlab.com/blog/2019/07/16/elasticsearch-update/); [Update: Elasticsearch lessons learnt for Advanced Global Search 2020-04-28 (April 2020)](https://about.gitlab.com/blog/2020/04/28/elasticsearch-update/); [Troubleshooting Elasticsearch](https://docs.gitlab.com/ee/administration/troubleshooting/elasticsearch.html) [↩](https://alexklibisz.com/2022/02/18/optimizing-postgres-trigram-search.html#fnref:gitlab-elasticsearch)