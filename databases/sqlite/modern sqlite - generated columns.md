---
created: 2024-07-09T12:36:20.665Z
updated: 2024-07-09T12:36:20.665Z
---
https://antonz.org/sqlite-generated-columns/

> Another common use case is to extract a certain JSON path into a separate column and optionally index it:

```sql
create table events (
    id integer primary key,
    event blob,
    etime text as (event ->> 'time'),
    etype text as (event ->> 'type')
);

create index events_time on events(etime);

insert into events(event) values
(jsonb('{"time": "2024-05-01", "type": "credit"}')),
(jsonb('{"time": "2024-05-02", "type": "debit"}')),
(jsonb('{"time": "2024-05-03", "type": "close"}'));

select etime, etype from events;
```