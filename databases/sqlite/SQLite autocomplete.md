[Nice article](https://simonwillison.net/2018/Dec/19/fast-autocomplete-search/) from Simon Willison on building an autocomplete search API from a datasette instance.

Gives me a neat idea for building a simple golang tool that will embed a read-only sqlite database and serve it as an API; only one file, and you could easily proxy an API endpoint to it