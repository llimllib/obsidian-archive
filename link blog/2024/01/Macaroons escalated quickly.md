https://fly.io/blog/macaroons-escalated-quickly/

Thomas Ptacek walks you through how you might construct a [macaroon](https://en.wikipedia.org/wiki/Macaroons_(computer_science)), which is a token similar to a JWT that has some neat properties. (And a few less brain-dead decisions than JWT tokens have...)

> The problem with simple bearer tokens, like browser cookies or JWTs, is that they’re prone to being stolen and replayed by attackers.

> ...With minimal ceremony and no additional API requests, a banking app Macaroon lets you authorize a request with a caveat like, I don’t know, `{'maxAmount': '$5'}`. I mean, something way better than that, probably lots of caveats, not just one, but you get the idea: a token so minimized you feel safe sending it with your request. Ideally, a token that only authorizes that single, intended request.

He then talks about how the thing he actually likes about them more is that because users can add conditions to their own tokens, reducing the work that Fly needs to do to just checking that the action requested by the user has the appropriate conditions in the macaroon.

Finally, he goes into third-party caveats, which I guess are encrypted tokens stored within the token? I didn't really follow this bit, which is a shame because it seems important.

If I ever have to get deeper into macaroons, I'll read it in detail and understand his code.

---

He links to [this podcast](https://securitycryptographywhatever.com/2021/08/12/what-do-we-do-about-jwt-with-jonathan-rudenberg/), in the transcript he says this, which I found useful:

> With a bearer token, I extract the user from the token. Then I go to my database and I say, what does this user allowed to do through all my database associations and things like that.
> 
> And that is not the macaroon model. The macaroon model is here’s a token. The only way this could have been issued is if the system said it was okay to issue this token cryptographically in the first place, just trust the token, just do it do what the token says you can do, it’s not exactly that, but like when you think about what the caveats are, you have to be careful.