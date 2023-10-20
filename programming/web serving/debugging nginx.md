To debug an [[nginx]] config, create a config file that looks something like this in a file called `test.conf`:

```nginx
daemon off;
error_log /dev/stdout notice;

events{}
http {
    server {
	    rewrite_log  on;
        access_log   /dev/stdout;
        listen       8080;
        server_name  localhost;

        location /test {
          rewrite ^/test(.*)$ /new-url/$1 redirect;
        }
    }
}
```

Add whatever `location` or other handlers you want to test, then launch it with `nginx -c $(pwd)/test.conf`. It will start foregrounded and log errors and accesses to stdout, serving on `localhost:8080`. It will also log rewrite handlers due to the `rewrite_log` directive.

Then you can test it with curl, ex:

```text
$ curl -v localhost:8080/testsomething
*   Trying 127.0.0.1:8080...
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET /testsomething HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.79.1
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 302 Moved Temporarily
< Server: nginx/1.21.6
< Date: Mon, 06 Jun 2022 19:49:16 GMT
< Content-Type: text/html
< Content-Length: 145
< Location: http://localhost:8080/new-url/something
< Connection: keep-alive
<
<html>
<head><title>302 Found</title></head>
<body>
<center><h1>302 Found</h1></center>
<hr><center>nginx/1.21.6</center>
</body>
</html>
* Connection #0 to host localhost left intact
```

If you look in the terminal window with nginx running, you'll see a couple log messages about the redirect:

```text
2022/06/06 15:49:16 [notice] 68533#0: *1 "^/test(.*)$" matches "/testsomething", client: 127.0.0.1, server: localhost, request: "GET /testsomething HTTP/1.1", host: "localhost:8080"
2022/06/06 15:49:16 [notice] 68533#0: *1 rewritten redirect: "/new-url/something", client: 127.0.0.1, server: localhost, request: "GET /testsomething HTTP/1.1", host: "localhost:8080"
```