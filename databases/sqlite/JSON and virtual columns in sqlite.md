https://antonz.org/json-virtual-columns/

> So far, so good. But `json_extract()` parses the text on each call, so for hundreds of thousands of records the query is slow. What should you do?

> Define virtual columns:

```sql
alter table events
add column object_id integer
as (json_extract(value, '$.object_id'));

alter table events
add column object text
as (json_extract(value, '$.object'));

alter table events
add column action text
as (json_extract(value, '$.action'));
```

> Build an index:

```sql
create index events_object_id on events(object_id);
```

Now the query works instantly:

```sql
select object, action
from events
where object_id = 11;
```

> Thanks to virtual columns, we almost have a NoSQL database ツ

very cool!