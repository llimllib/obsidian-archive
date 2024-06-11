---
updated: 2024-06-11T19:49:39.601Z
created: 2024-03-04T19:22:32Z
---
Wanted to install it on my billmill.org server:

```
sudo apt install goaccess
```

Next I need to figure out where my access log is. `systemctl status caddy` reminded me that my caddy config file is at `/etc/caddy/Caddyfile`. It seems that I'm maybe not writing access logs at all?

Following the [docs](https://caddyserver.com/docs/caddyfile/directives/log),

```
$ sudo mkdir /var/log/caddy
# edit the caddy log file to add:
#    log {
#        output file /var/log/caddy/access.log {
#            roll_size 10MB
#            roll_keep 5
#        }
#    }
$ sudo systemctl restart caddy
```

now `systemctl status caddy` shows caddy running, but there's sitll nothing in the /var/log/caddy directory. Ah ha, the status logs show the error: `write error: can't open new logfile: open /var/log/caddy/access.log: permission denied`

So, `chmod a+rw /var/log/caddy/` and 💥 caddy now logs accesses

ugh, of course debian has an ancient version of goaccess. it doesn't handle caddy format. Their [download page](https://goaccess.io/download)

recommends this process:

```
wget -O - https://deb.goaccess.io/gnugpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/goaccess.gpg >/dev/null
echo "deb [signed-by=/usr/share/keyrings/goaccess.gpg] https://deb.goaccess.io/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/goaccess.list
sudo apt-get update
sudo apt-get install goaccess
```

So after a `apt remove goaccess`, let's give it a try... and it seemed to go fine, but installed the same ancient version.

I'm on a modern version of ubuntu (20.04), but it seems not to be finding the package for whatever reason. blugh.

ok, fine, let's install go:

```
wget https://go.dev/dl/go1.18.1.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.18.1.linux-amd64.tar.gz
```

Then build goaccess:

```
wget https://tar.goaccess.io/goaccess-1.5.7.tar.gz
tar -xzvf goaccess-1.5.7.tar.gz
cd goaccess-1.5.7/
# install deps because configure failed
apt install libncursesw5-dev libgeoip-dev libmaxminddb-dev libssl-dev
# try configure again
./configure --enable-utf8 --enable-geoip=mmdb
make
make install
```

ok, installed, but get an error! seems to be https://github.com/allinurl/goaccess/issues/2308 ; goaccess got updated for a more recent version of caddy, but that breaks processing for older versions of caddy.

```
root@billmill:~# goaccess /var/log/caddy/access.log --log-format=CADDY
Cleaning up resources...
==1316640== GoAccess - Copyright (C) 2009-2020 by Gerardo Orellana
==1316640== https://goaccess.io - <hello@goaccess.io>
==1316640== Released under the MIT License.
==1316640==
==1316640== FILE: /var/log/caddy/access.log
==1316640== Parsed 10 lines producing the following errors:
==1316640==
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640== IPv4/6 is required.
==1316640==
==1316640== Format Errors - Verify your log/date/time format
```

so I'll try the same install dance with goaccess 1.5.6. Hey finally it works!

```
goaccess /var/log/caddy/access.log --log-format=CADDY
```

Fires up a nice curses TUI. There's probably a way to get the web UI up and running, but that's fine enough for me - I can just ssh in.

If I ever want to get it running as a service, [this comment](https://github.com/allinurl/goaccess/issues/1898#issuecomment-685727741) ) may serve as a starting point for running it as a systemd service. Next up I'd have to figure out how to proxy it back out through caddy.

- [this page](https://cristianpb.github.io/blog/traefik-goaccess) has a systemd service that specifies inline config

[this webpage]() suggests this command:

```console
goaccess --log-format=VCOMMON \
         --ws-url=wss://stats.example.com/ws \
         --output=${STATS_DIR}/index.html \
         --log-file=/etc/logs/requests.log \
         --no-query-string \
         --anonymize-ip \
         --double-decode \
         --real-os \
         --real-time-html
```

and this caddy config to proxy it back out:

```conf
https://stats.example.com/ws {
    proxy / localhost:7890 {
       websocket
    }
}```
```

This worked for getting a webserver up and running: `goaccess /var/log/caddy/access.log --log-format=CADDY -o /var/www/html/_goaccess.html --real-time-html`

github [code search](https://cs.github.com/?scopeName=All+repos&scope=&q=goaccess+path%3ACaddyfile) has a few examples, including one that puts it behind a basic auth, which seems sensible

---

How to pas a directory of access files, some of which are gz encoded and some are not, into goaccess:

`zcat -f /var/log/caddy/access* | goaccess - --log-format=CADDY`

It takes a bit to process them, but it will load them all and display your stats over time