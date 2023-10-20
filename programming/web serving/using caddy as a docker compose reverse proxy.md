## part 1: plain old HTTP

Say you have a `docker-compose.yml` file containing a service that you'd like to proxy both https and http traffic to:

```yaml
version: '3'
services:
  httpbin:
    image: mccutchen/go-httpbin
    command: ['/bin/go-httpbin', '-port', '8080']
```

_this service runs [go-httpbin](https://github.com/mccutchen/go-httpbin) on port 8080_

First, we can write a `Caddyfile` that reverse proxies all plain http requests (anything on port 80) to our service:

```
:80 {
  reverse_proxy httpbin:8080
}
```

And add a reverse proxy service using [[caddy]] to our docker-compose file:

```yaml
services:
  # ...snip...
  reverse_proxy:
    image: caddy
    depends_on:
      - httpbin
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
    ports:
      - "80:80"
```

This creates a service using the `caddy` docker hub image, which will start up `httpbin` as a dependency, and use the `Caddyfile` we defined a moment ago to proxy HTTP requests to `httpbin`, and sets it to expose port 80 to the host (i.e., your computer).

(If port 80 is not available on your computer, you can change the first `80` to something that is available for testing this service)

You can test that it works by:
- starting the service with `docker up reverse_proxy`
- then, running `curl http://localhost/uuid` in another terminal
	- you can visit `http://localhost` in your browser to see many more endpoints available to you

```console
$ curl http://localhost/uuid
{
  "uuid": "ea19ff33-c0cf-402e-afb7-bb820055d5c2"
}
```

_Success!_

All the files for part 1 are available [here](https://github.com/llimllib/personal_code/tree/eaaa795cb19f45054efff42d31a01d290bd0bb38/misc/docker-caddy-reverse-proxy/part1)

## part 2: proxying TLS

Next up, let's set up TLS so that `curl https://localhost/uuid` will work.

My favorite tool for generating certificates is [mkcert](https://github.com/FiloSottile/mkcert) by the excellent Filippo Valsorda. Let's install it (on my mac it's `brew install mkcert`, your system may vary), then generate some certs we can use:

```console
$ mkcert localhost
Note: the local CA is not installed in the system trust store.
Note: the local CA is not installed in the Firefox trust store.
Run "mkcert -install" for certificates to be trusted automatically ⚠️

Created a new certificate valid for the following names 📜
 - "localhost"

The certificate is at "./localhost.pem" and the key at "./localhost-key.pem" ✅

It will expire on 23 September 2025 🗓
```

And we can see that it generated certificates in files `localhost.pem` and `localhost-key.pem` in the current directory, but also told us that the CA used to generate these certificates is not available in our local trust store. This means that if we were to use them to serve traffic from our reverse proxy right now, our browser would tell us that we were visiting a possibly malicious site because it didn't know to trust the certificates.

Let's follow the instructions and install the certificates to our trust store:

```console
$ mkcert -install
The local CA is now installed in the system trust store! ⚡️
The local CA is now installed in the Firefox trust store (requires browser restart)! 🦊
```

And now, our certificates should work once they're used somewhere. 

Next up, we want to tell caddy to serve traffic on port `443` (the default HTTPS port) using these certificates. First let's:

- move our generated certificates into a `keys` folder, for cleanliness. `mkdir keys && mv localhost* keys`
- mount the `keys` folder into the caddy container so that caddy has access to the certificates:

```yaml
  reverse_proxy:
    image: caddy
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - httpbin
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - ./keys:/keys
```

Then we should update our Caddyfile to tell caddy to reverse proxy TLS using the generated certificates:

```
:80 {
  reverse_proxy httpbin:8080
}

:443 {
  tls /keys/localhost.pem /keys/localhost-key.pem
  reverse_proxy httpbin:8080
}
```

Now if we start the service up again with `docker compose up`, we should be able to use `curl` in another terminal to access our service via https:

```
$ curl https://localhost/uuid
{
  "uuid": "b11d7330-3cac-44d2-b3f3-ac295adc8ee5"
}
```

Success!

All the files for part 2 are available [here](https://github.com/llimllib/personal_code/tree/eaaa795cb19f45054efff42d31a01d290bd0bb38/misc/docker-caddy-reverse-proxy/part2)

## part 3: getting other services access

We're now successfully proxying https traffic from our host machine to a service in a docker compose network via both https and http, but we may also want to have other services in the docker compose network be able to access the service.

To do a really simple test, let's add a `test` service that has curl, which we can use to make requests:

```yaml
  test:
    image: curlimages/curl
    depends_on:
      - reverse_proxy
```

Here's how we can make a request inside the docker-compose network to the `reverse_proxy` service:

```console
$ docker compose run test sh -c 'curl http://reverse_proxy/uuid'
[+] Running 2/0
 ⠿ Container part3-httpbin-1        Running                                                                0.0s
 ⠿ Container part3-reverse_proxy-1  Running                                                                0.0s
{
  "uuid": "46c45810-40b7-4af7-bf10-673882a4864f"
}
```

And that works! hooray. 

However, if we try to make a request to `https` instead of `http`, we'll get a failure:

```console
$ docker compose run test sh -c 'curl https://reverse_proxy/uuid'
[+] Running 2/0
 ⠿ Container part3-httpbin-1        Running                                                                0.0s
 ⠿ Container part3-reverse_proxy-1  Running                                                                0.0s
curl: (60) SSL certificate problem: unable to get local issuer certificate
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```

This failure occurs because the operating system inside the container does not yet trust the certificates we generated earlier.

We could tell curl just to forget about verifying the certificates, using the aptly named `--insecure` flag:

```console
$ docker compose run test sh -c 'curl --insecure https://reverse_proxy/uuid'
[+] Running 2/0
 ⠿ Container part3-httpbin-1        Running                                                                0.0s
 ⠿ Container part3-reverse_proxy-1  Running                                                                0.0s
{
  "uuid": "4cb47207-b80c-4703-9fe2-62f76dfe5ea1"
}
```

But that's an unsatisfying answer. We can do better by installing our CA certificate into the trust store of the container.

First we need to get the CA certificate, which `mkcert` will helpfully tell us the location of, and copy it into the `keys` folder we made earlier:

```console
cp "$(mkcert -CAROOT)/rootCA.pem" ./keys/
```

Next, we need to add that CA certificate to the trust store on our `test` container.

Unfortunately, there's no one-size-fits all solution for doing this; for every container you want to trust a given CA certificate you'll have to figure out how to trust it. In this case, we're going to write a short Dockerfile to create an alpine-based container with `curl` installed and our CA certificate trusted:

```Dockerfile
FROM alpine:3.18

# copy the CA we want to trust into a location where alpine expects it to be
COPY keys/rootCA.pem /usr/local/share/ca-certificates/

# tell alpine to trust the CA file we added
RUN apk --no-cache add ca-certificates curl && \
  rm -rf /var/cache/apk/* && \
  update-ca-certificates
```

We'll save that file to `curl.Dockerfile`, and update the `test` service to use it:

```yaml
  test:
    build:
      context: .
      dockerfile: curl.Dockerfile
    depends_on:
      - reverse_proxy
```

Now we're closer, but there's still a snag; the certificates we generated earlier were generated for a server named `localhost`, not for a server named `reverse_proxy`:

```console
$ docker compose run --build test sh -c 'curl https://reverse_proxy/uuid'
... snip build output...
curl: (60) SSL: no alternative certificate subject name matches target host name 'reverse_proxy'                
More details here: https://curl.se/docs/sslcerts.html                                                           

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```

Way back when, we generated our cert with `mkcert` and told it to generate them for localhost; now we can regenerate our certificates, but add `reverse_proxy` as a valid name:

```console
$ mkcert localhost reverse_proxy && mv *-key.pem ./keys/localhost-key.pem && mv *.pem ./keys/localhost.pem 

Created a new certificate valid for the following names 📜
 - "localhost"
 - "reverse_proxy"

The certificate is at "./localhost+1.pem" and the key at "./localhost+1-key.pem" ✅

It will expire on 23 September 2025 🗓
```

At this point you may have to run  `docker compose down` so that our running `reverse_proxy` will restart and pick up the new keys.

Then, we can run a command in our `test` container, and see that it went through!

```console
$ dc run --build test sh -c 'curl https://reverse_proxy/uuid'
# snip lots of build output
{
  "uuid": "6af7ac8c-9312-4cc2-990c-5dacbcdb62a3"
}
```

All the files for part 3 are available [here](https://github.com/llimllib/personal_code/tree/master/misc/docker-caddy-reverse-proxy/part3)