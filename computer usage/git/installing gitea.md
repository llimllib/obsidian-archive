https://docs.gitea.io/en-us/install-from-binary/

- create user:

```shell
adduser \
   --system \
   --shell /bin/bash \
   --gecos 'Git Version Control' \
   --group \
   --disabled-password \
   --home /home/git \
   git
```

- create directories and set permissions:

```shell
mkdir -p /var/lib/gitea/{custom,data,log}
chown -R git:git /var/lib/gitea/
chmod -R 750 /var/lib/gitea/
mkdir /etc/gitea
chown root:git /etc/gitea
chmod 770 /etc/gitea

# > NOTE: /etc/gitea is temporary set with write rights for user git so that Web installer could write configuration file. After installation is done, it is recommended to set rights to read-only using:

# > chmod 751 /etc/gitea
# > chmod 640 /etc/gitea/app.ini
```

- download the most recent binary:

```shell
wget https://dl.gitea.io/gitea/1.17/gitea-1.17-linux-amd64
mv gitea-1.17-linux-amd64 gitea
mv gitea /usr/local/bin/
```

- next up, let's create a service file to run it
- https://docs.gitea.io/en-us/linux-service/
- https://github.com/go-gitea/gitea/blob/db3355cb1aa206fc9f1cf786543607204f628218/contrib/systemd/gitea.service

```shell
# create this file and copy in the contents
vim /etc/systemd/system/gitea.service

# enable it (we're already root, no need to sudo)
root@billmill:~# systemctl enable gitea
Created symlink /etc/systemd/system/multi-user.target.wants/gitea.service → /etc/systemd/system/gitea.service.

# start it
systemctl start gitea

# view it
systemctl status gitea
```

- looks like it's listening on port 3000 by default:

```shell
root@billmill:~# lsof -i -P -n | grep gitea
gitea     1587950             git    6u  IPv6 26317531      0t0  TCP *:3000 (LISTEN)
```

- let's reverse proxy to it:
- https://docs.gitea.io/en-us/reverse-proxies/

```shell
# reverse proxy to gitea
gitea.billmill.org {
    reverse_proxy 127.0.0.1:3000
}
```

- OK! Now https://gitea.billmill.org/ brings up a config page (I had previously pointed the subdomain DNS to my web host)
  - for some reason on firefox this doesn't properly work, I don't know how to tell it to try DNS again
	  - or maybe this is because firefox is doing the dns over https thing and it hasn't propagated there?

- I'm not setting up email at this time
  - I kind of want to enable "allow registration only through external services", but I'm not sure what services are available?
  - config reference: https://docs.gitea.io/en-us/config-cheat-sheet/
  - config is at `/etc/gitea/app.ini`

- When I log in it wants a password, let's try to get ssh config set up
  - create a key (locally), default options:

ssh-keygen -t ed25519

- meh let's just use un/pw for now, our credential store should save them in keychain
  - I started down the road of enabling ssh but it becomes a user management thing I'd rather not deal with
	  -  or maybe if I could get gitea's ssh server going it wouldn't be painful? but not going to deal with it for now