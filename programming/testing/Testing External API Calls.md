https://www.cosmicpython.com/blog/2020-01-25-testing_external_api_calls.html

Provides a similar perspective as [[don't mock what you don't own]], advises creating adapter objects for external APIs so that you can substitute test adapters more clearly than mocking the actual external API.

Seems wise to me, having suffered the pain of directly testing APIs.