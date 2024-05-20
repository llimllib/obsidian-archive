---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://words.filippo.io/how-plex-is-doing-https-for-all-its-users/

Interesting dive into how Plex is creating certs for every plex server

> This way when a server first starts it asks for its wildcard certificate to be issued (which happened almost instantly for me) and then the client, instead of connecting to `http://1.2.3.4:32400`, connects to `https://1-2-3-4.625d406a00ac415b978ddb368c0d1289.plex.direct:32400` which **resolves to the same IP, but with a domain name that matches the certificate** that the server (and only that server, because of the hash) holds.

found via [this tweet](https://twitter.com/FiloSottile/status/1529377551990366209)

> The end of DNS rebinding is nigh! With a bit of luck and some time, maybe it will also mean DNS resolvers can stop breaking public domains that resolve to internal addresses, making [https://words.filippo.io/how-plex-is-doing-https-for-all-its-users/](https://t.co/QSM609FylN) more viable!

The point about this in his article is:

> P.S.: I finally figured out why they advise you might need to turn off _DNS rebinding_ protections: a domain like `192-168-1-7.###.plex.direct` which resolves to a local IP (that they use when you want to connect to a server on your LAN while still using the HTTPS web app) is exactly what a rebinding attack needs to access vulnerable services behind your firewall. See for example [this post by Michele Spagnuolo](https://miki.it/blog/2015/4/20/the-power-of-dns-rebinding-stealing-wifi-passwords-with-a-website/).



