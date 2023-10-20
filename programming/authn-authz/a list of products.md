- Ory kratos
	- https://github.com/ory/kratos
	- Next-gen identity server (think Auth0, Okta, Firebase) with Ory-hardened authentication, MFA, FIDO2, profile management, identity schemas, social sign in, registration, account recovery, and IoT auth. Golang, headless, API-only - without templating or theming headaches.
	- Ory is the only identity platform that can scale indefinitely and is based entirely on open source.
		- ory.sh
	- intro docs: https://www.ory.sh/kratos/docs/

- [Authelia](https://github.com/authelia/authelia)
	- The Single Sign-On Multi-Factor portal for web apps
	- **Authelia** is an open-source authentication and authorization server providing two-factor authentication and single sign-on (SSO) for your applications via a web portal. It acts as a companion for reverse proxies like [nginx](https://www.nginx.com/), [Traefik](https://traefik.io/) or [HAProxy](https://www.haproxy.org/) to let them know whether requests should either be allowed or redirected to Authelia's portal for authentication.
	- [![](https://github.com/authelia/authelia/raw/master/docs/images/archi.png)](https://github.com/authelia/authelia/blob/master/docs/images/archi.png)
	- includes docker-compose files which look helpful in getting it up and running

- [Keratin](https://github.com/keratin/authn-server)
	- Authentication service that keeps you in control without forcing you to be an expert in web security.
	- strictly focuses on authn, not authz
	- This repository builds a backend Go service that provides secured endpoints related to accounts and passwords. You must integrate it with your application's frontend(s) and backend(s).

- [Keycloak](https://www.keycloak.org/)
	- Add authentication to applications and secure services with minimum fuss. No need to deal with storing users or authenticating users. It's all available out of the box.
	- https://github.com/keycloak/keycloak
	- Open Source Identity and Access Management For Modern Applications and Services
	- seems to require a java runtime
	- news.yc comments suggest it's very capable but difficult to understand and heavyweight: https://news.ycombinator.com/item?id=31258469

- [Cognito](https://aws.amazon.com/cognito/)
	- I had a hell of a time getting started with it in the past
	- https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-getting-started.html

- [GoTrue](https://github.com/netlify/gotrue)
	- GoTrue is a small open-source API written in Golang, that can act as a self-standing API service for handling user registration and authentication for Jamstack projects.
	- It's based on OAuth2 and JWT and will handle user signup, authentication and custom user data.

- [Kanidm](https://github.com/kanidm/kanidm)
	- Kanidm: A simple, secure and fast identity management platform
	- still an alpha, not ready for prime time, including it on the list just to watch

- [NetAuth](https://github.com/netauth/netauth)
	- NetAuth is a network identity and authentication provider. It allows you to have one user account that is available to a lot of different machines.
	- The ultimate goal is to have a small service which could live in a small VM and provide fleet wide authentication and identity services for a small fleet of machines.
	- communicates with gRPC/protobuf

- [Oso](https://github.com/osohq/oso)

- [Casdoor](https://casdoor.org/)
	- A UI-first centralized authentication / Single-Sign-On (SSO) platform supporting OAuth 2.0, OIDC and SAML, integrated with Casbin RBAC and ABAC permission management
	- looks to be pertty darn mature, provides a lot of providers
	- Works with authorization service [casbin](https://github.com/casbin/casbin)

- [Aserto](https://www.aserto.com/)
	- Opinionated framework that covers everything you need to build RBAC
	- REST/gRPC API’s with native support for popular languages and frameworks
	- Flexible deployment model - hosted service, local service, or sidecar
	- Open source authorizer based on CNCF Open Policy Agent

- [Zitadel](https://github.com/zitadel/zitadel/)
	- ZITADEL - The Open Source Auth0, Firebase Auth, AWS Cognito and Keycloak alternative written in Go and built for the serverless era
	- We built **ZITADEL** around the idea that the IAM should be easy to deploy and scale. That's why we tried to reduce external systems as much as possible.

- [spicedb](https://github.com/authzed/spicedb)
	- SpiceDB is an open source database system for managing security-critical application permissions inspired by Google's [Zanzibar](https://authzed.com/blog/what-is-zanzibar/) paper.
	- Developers create a schema that models their permissions requirements and use a [client library](https://github.com/orgs/authzed/repositories?q=client+library) to apply the schema to the database, insert data into the database, and query the data to efficiently check permissions in their applications.

- [clerk](https://clerk.com)
	- Clerk is more than a “sign-in box”. Integrate complete user management UIs and APIs, purpose-built for React, Next.js, and the Modern Web.
	- via [tmcw](https://elk.pwm.social/hachyderm.io/@tmcw@bird.makeup/110181774794665316), who is using it for val.town