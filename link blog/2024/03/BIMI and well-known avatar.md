TIL that [there is a spec called BIMI](https://shkspr.mobi/blog/2022/08/dns-esoterica-bimi-svg-in-dns-txt-wtf/) that is supposed to allow you to pair a logo with your URL via DNS. Unfortunately it costs more than a thousand dollars to sign up and doesn't work that well, so nobody uses it.

In semi-related news, Terence Eden [proposes](https://shkspr.mobi/blog/2024/03/well-known-avatar/) `.well-known/avatar`:

> When I sign up to a web service, I don't want to faff around uploading an image to use as my avatar. I want that service to look at my email address or social-sign-in and automatically pick up my preferred graphic.

> Here's how I see it working.

> 1. A user signs in to a service with the email address `username@example.com`
> 2. In a similar way to [WebFinger](https://www.rfc-editor.org/rfc/rfc7033), the service makes a request to:
    - `example.com/.well-known/avatar?resource=acct:username@example.com`
> 3. If the request's `Accept` header has a MIME type of `image/*`, then the server immediately returns an image.
> 4. If the request's `Accept` header has a MIME type of `application/json`, then the server can return a WebFinger-style document with [`"rel":"http://webfinger.net/rel/avatar"`](https://webfinger.net/rel/#avatar) and, perhaps, a list of different images, formats, and sizes.

Both links via [mastodon](https://mastodon.social/@Edent/112111052673785598)