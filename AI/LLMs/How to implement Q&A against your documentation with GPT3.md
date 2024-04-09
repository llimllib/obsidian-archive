https://simonwillison.net/2023/Jan/13/semantic-search-answers/

-   Run a text search (or a semantic search, described later) against your documentation to find content that looks like it could be relevant to the user’s question
-   Grab extracts of that content and glue them all together into a blob of text
-   Construct a prompt consisting of that text followed by “Given the above content, answer the following question: ” and the user’s question
-   Send the whole thing through [the GPT-3 API](https://beta.openai.com/docs/api-reference/completions) and see what comes back

I’ve been calling this the **semantic search answers** pattern.

> **Update:** Since publishing this post I’ve learned that this technique is known as **Retrieval-Augmented Generation** or RAG, as described in [this paper from May 2020](https://arxiv.org/abs/2005.11401). I’ve also been pointed to the [Question Answering using Embeddings](https://github.com/openai/openai-cookbook/blob/main/examples/Question_answering_using_embeddings.ipynb) notebook in the OpenAI cookbook which describes this same technique.