---
created: 2026-05-01T11:49:09.634Z
updated: 2026-05-01T11:49:09.634Z
---
(The content of this chapter is kind of basics of what I've been doing for a long time now, so my notes will be skimpy)

ORMs: maybe good, maybe bad

They talk about the tradeoffs of using a JSON document rather than tables, and I think it's funny that after talking about how nice it is to have one-to-many represented in a document, say that if you have a lot of references you might be better off with a table

`When you use an ID, your data is more normalized`, lol the water under that statement is deep

I'm actually surprised that they talk about the document vs relational database tradeoff more in terms of normalization & joins than they do about schemas vs schemaless, to me that's at least as important a concern.

Also, they previously talked about fanout, and are kind of hinting at the connection between denormalized data and fanout, but aren't making it explicit (nvm, they do that immediately after this occurred to me)

Can feel the author's pain in writing `X (formerly Twitter)`. How many years will we still write `(formerly Twitter)`?

> The process of looking up the human-readable information by ID is called _hydrating_ the IDs

`hydrating` is a seriously overused phrase in the web world!

> If you need to decide whether to denormalize something in your application, the social network case study shows that the choice is not immediately obvious; the most scalable approach may involve denormalizing some things and leaving others normalized

amen! I wonder if I could come up with a better way to help people (myself) see a web serving system as a series of buffers and channels as a mechanism for thinking through tradeoffs better.

For example, something they don't mention is that the reason it's convenient to _hydrate_ tweet IDs - and in fact that I think they possibly get a bit wrong or at least unclear - is that they're embarrassingly cacheable and we can rely on the global CDN network to act as a giant buffer preventing requests to our system.

Furthermore, if we treat the CDN system as a database, we actually have denormalized our tweet ID -> content database in a way! We've fanned it out across however many servers are in the CDN network.

Recursion all the way down, forever

## Stars and Snowflakes: Schemas for Analytics

This part is actually new to me, I know jack all about analytics DBs.

The last time I read about a _star schema_, it was about Ethernet network topology

In this case, they mean one very large table ("fact table") consisting mostly of many references; the example they give is of a `sales` table for a grocery store, where each row of the table relates to customer, product, etc etc and the table grows very large over time.

A _snowflake schema_ is the same thing, but the tables the main table references are themselves composed of references

## When to use which model

They note the difficulty of maintaining an ordered list without a document, which is fair - it's kind of comical how difficult it still is to store an ordered list of items in a relational table without reaching for a document

Honestly this is a section of a chapter that could be a whole book

Finally they talk about schemas here:

> Document databases are sometimes called _schemaless_, but that's misleading as the code that reads the data usually assumes some kind of structure -- that is, there is an implicit schema, but it is not usually enforced by the database. A more accurate term is _schema-on-read_ (the structure of the data is implicit and interpreted only when the data is read), in contrast with _schema-on-write_

I've never heard _schema-on-read_ before! I guess my question is, in what sense can we say that the data has a schema? My experience with a production service running on Mongo is that the only sense there is a schema is that we randomly scatter exception handling and hope maybe we get a useful error when we read data that doesn't match.

Oddly, in the same service we _also_ had the opposite problem, of the schema-on-read type-checking infrastructure becoming a thick network of ivy overgrowing our codebase

> The difference between the approaches is particularly noticeable when an application wants to change the format of its data

in that service, the answer was "you just don't ever change it". Or, you change it going forward but not backward (because it was impossible to change owing to no schema), and hope that future people maybe can get lucky and find the data they want.

