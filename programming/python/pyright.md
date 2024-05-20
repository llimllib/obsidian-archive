---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
[useful documentation](https://github.com/microsoft/pyright/blob/main/docs/type-concepts.md#debugging-inferred-types) on using the type checker

Especially useful is the `reveal_type` function, which will show you the type that pyright has inferred. For example:

![[Pasted image 20221014093101.png]]

In this case, I used that statement to reveal that I needed to narrow the type to `str` so that pyright wouldn't flag the `BeautifulSoup` call as incorrect.