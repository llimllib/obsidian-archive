---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
@tqbf on twitter asked:

> Has anyone ever written up CLI-to-web authentication flows, like the one Heroku did, or the one Teleport does? I’m wondering if there’s best practices and stuff.

we chatted a bit - I had copied his code for doing this process - when Patrick Toomey (security guy at github, according to his bio, I feel like I might recognize the name but can't think of from where?) [responded with](https://twitter.com/patricktoomey/status/1513713615093727235):

> Are we not largely talking about this - [https://datatracker.ietf.org/doc/html/rfc8628](https://t.co/28g2LBvVA2) ?

That RFC is for an `OAuth 2.0 Device Authorization Grant`: and it's basically the process that Apple TV apps, and the github and AWS CLI (I think) follow:

- User initiates a login
- CLI presents a URL to visit and a code to enter
- User goes to URL, logs in if necessary, enters the code from the CLI
- Github asks you to grant the token scopes once this is successful - TV apps and Amazon just assume you're logged in if you entered the correct code
	- Amazon actually doesn't even make you enter the code if you're already logged in with the browser - it seems to just extend your session

I spent some time trying to see if [devise](https://github.com/heartcombo/devise) or [omniauth](https://github.com/omniauth/omniauth) supported this flow, and wasn't able to find any evidence that they did.

I did find [this rails library, exop-group/doorkeeper-device_authorization_grant](https://github.com/exop-group/doorkeeper-device_authorization_grant) but that would require using [a different oauth lib](https://github.com/doorkeeper-gem/doorkeeper) than the one we're using already.

[Elsewhere](https://twitter.com/patricktoomey/status/1513715981331230721) in the thread, Patrick mentions that the GH CLI uses polling, not opening a local web server:

> The device authorization flow doesn’t use a localhost listener…it’s polling based. The localhost pattern is separate.

Google [appears to have](https://developers.google.com/identity/protocols/oauth2/limited-input-device) semi-deprecated the device flow, limiting its available scopes and preferring [an alternate flow](https://developers.google.com/identity/protocols/oauth2/native-app) for reasons that are unclear to me.

[here](https://docs.aws.amazon.com/singlesignon/latest/OIDCAPIReference/Welcome.html) is some AWS docs on SSO; I found that via [this](https://github.com/aws/aws-sdk-ruby/blob/09f32a45dded28c33062d6c9a3440abeb66b47ac/gems/aws-sdk-ssooidc/lib/aws-sdk-ssooidc/types.rb#L48) aws sdk code

[this article](https://developer.okta.com/blog/2019/02/19/add-oauth-device-flow-to-any-server) helped me understand it a bit, and to verify by searching for `device_code` in ruby code that there does not appear to be a ruby server-side implementation of it as far as I can tell.