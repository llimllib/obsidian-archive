https://github.com/hgrsd/drivel

> `drivel` is a command-line tool written in Rust for inferring a schema from an example JSON (or JSON lines) file, and generating synthetic data (the drivel in question) based on the inferred schema.

Very cool.

> In 'describe' mode, drivel infers the schema from the input JSON and prints a human-readable description of the schema. This mode is useful for understanding the structure and data types present in JSON data.

Related: [[jless]], [[gron]], [[jnv]]

> Consider a JSON file `input.json`:

```json
{
  "name": "John Doe",
  "id": "0e3a99a5-0201-4444-9ab1-8343fac56233",
  "age": 30,
  "is_student": false,
  "grades": [85, 90, 78],
  "address": {
    "city": "New York",
    "zip_code": "10001"
  }
}
```

> `cat input.json | drivel describe`

```
{
  "age": int (30),
  "address": {
    "city": string (8),
    "zip_code": string (5)
  },
  "is_student": boolean,
  "grades": [
    int (78-90)
  ] (3),
  "name": string (8),
  "id": string (uuid)
}
```

via [mastodon](https://hachyderm.io/@hgrsd/112196338504223975)