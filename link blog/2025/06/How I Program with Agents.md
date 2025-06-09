> Let me talk you through an example of where I used an agent to do a significant amount of work on a project. I implemented the first pass of Github App auth for the hosted sketch.dev using sketch. It did the whole thing with 3-4 pieces of feedback as I clicked around the interface finding errors. That is an astonishing achievement. It is easy for the haughty to disregard the work of gluing well-known APIs together as “not real” programming, but it has been the practical experience of my career that for every hour of truly interesting programming I can do, I have had to do 10 or more hours of dreary work with APIs, libraries, dysfunctional compilers, build systems, or obtuse package managers to actually make that hour useful. Having a tool that lets me do 30 minutes of “not real” programming by writing a few carefully constructed sentences, and lets me vacuum the kids' room while it works, **preserves momentum**.

David Crawshaw follows up on [[How I program with LLMs]], and it's just as interesting.

Also, this is pretty interesting and kind of wild:

> I learned an odd way of using SQL at Tailscale (from Brad and Maisem): make every table a JSON object. In particular, have only one “real” column and the rest generated from the JSON. So the typical table looks like:

```sql
CREATE TABLE IF NOT EXISTS Cookie (  
  Cookie   TEXT    NOT NULL AS (Data->>'cookie')  STORED UNIQUE, -- PK
  UserID   INTEGER NOT NULL AS (Data->>'user_id') STORED REFERENCES User (UserID),  
  Created  INTEGER NOT NULL AS (unixepoch(Data->>'created')) STORED,  
  LastUsed INTEGER AS (unixepoch(Data->>'last_used')) CHECK (LastUsed>0),  
  Data     JSONB   NOT NULL  
);
```

> This has many pros and many cons. It acts as a poor man’s ORM as each table has an “obvious” data type matching each record. It makes adding to the schema trivial. You can choose to ADD COLUMN if you like but you do not have to. The SQL column constraints act as good dynamic checks on the quality of your JSON. It greatly increases the amount of stored data per row. You have to structure all your INSERT and UPDATEs in terms of JSON. Half a foot in the document database world, but I can still write an old fashioned JOIN. Etc.

I had to read that SQL snippet a few times to get what was going on there! *(It's creating derived columns from the final `Data` column)*

> The way this all works today is very different than six months ago, and I do not believe we are at a stable point yet. I believe a lot of norms around team interactions will also be changing. For example, **the mostly-broken process of half-hearted code review that has been adopted across the industry no longer solves the problems it barely solved before**. It needs to be reinvented