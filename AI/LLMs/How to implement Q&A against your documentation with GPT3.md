https://simonwillison.net/2023/Jan/13/semantic-search-answers/

-   Run a text search (or a semantic search, described later) against your documentation to find content that looks like it could be relevant to the user’s question
-   Grab extracts of that content and glue them all together into a blob of text
-   Construct a prompt consisting of that text followed by “Given the above content, answer the following question: ” and the user’s question
-   Send the whole thing through [the GPT-3 API](https://beta.openai.com/docs/api-reference/completions) and see what comes back

I’ve been calling this the **semantic search answers** pattern.