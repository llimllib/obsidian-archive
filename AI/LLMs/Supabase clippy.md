---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://supabase.com/blog/chatgpt-supabase-docs

Supabase implemented a gpt-based search for their docs.

This video is super helpful in explaining how they did it:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Yhtjd7yGGGA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Basically they 1. search (normally) for relevant context in their docs 2. Include that as context in the prompt ("prompt injection"), then query gpt with it