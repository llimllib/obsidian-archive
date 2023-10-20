https://fly.io/blog/skip-the-api/

> A different approach is to skip the API design entirely and just ship the entire database to your client. You don’t need to consider the consuming service’s access patterns as they can use vanilla SQL to query and join whatever data their heart desires. That’s what we did using LiteFS.

> ...Pushing queries out to the end user has huge benefits for both the data provider & the data consumer in terms of flexibility and power.

The article doesn't give me a very good picture of exactly what fly has done in this instance, but the idea of breaking apart the database and using sqlite files instead of an API is what has had me so excited about sqlite for a while.

I think there are very interesting architectures that we're not trying out because we have a mechanism that works - central database + API layer - but that would have benefits in many applications.

Or maybe not! But I look forward to more experiments like this.