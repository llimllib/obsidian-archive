---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
1. buy a domain name
2. point the nameservers to digital ocean
3. create a DO droplet
4. point pwm.social and www.pwm.social towards that droplet with A records on the DO control panel
5. DNS doesn't resolve yet, log into box with `ssh user@ip`
6. [install docker](https://docs.docker.com/engine/install/ubuntu/)
7. [install caddy](https://caddyserver.com/docs/install#debian-ubuntu-raspbian)
8. Create takahe config in a file called `takahe.conf`, see below for the fields and format.
	1. Note importantly that you _can't_ surround the strings with quotes because this is a docker env file, not a bash script! This bit me.
9. Run takahe backend with:
```
docker run \
  --env-file takahe.conf \
  --volume /Users/llimllib/.config/gcloud/:/creds \
  -p 8001:8001 \
  jointakahe/takahe
```
10. Run stator with:
```
docker run \
  --env-file takahe.conf \
  --volume /Users/llimllib/.config/gcloud/:/creds \
  jointakahe/takahe python3 manage.py runstator
```
11. Configure caddy to proxy back to port 8001:
```
www.yoursite.social {
	handle {
		# proxy to takahe
		reverse_proxy qfwfq:8001
	}
}
```
12. Visit https://www.yoursite.social; if all went well you'll be looking at the takahe home screen
13. Register a user with the username you set in `TAKAHE_AUTO_ADMIN_EMAIL`
	1. Or, run `docker run --rm -it --env-file takahe.conf jointakahe/takahe python3 manage.py createsuperuser`, which is what I did
14. You should now have a running Takahe server!

## config sample

I got the site running with a config like this one:

```
TAKAHE_DATABASE_SERVER=postgres://user:pass@host:port/database_name
TAKAHE_SECRET_KEY=<long random string>
TAKAHE_MEDIA_BACKEND=gs://<bucket-name>
TAKAHE_MAIN_DOMAIN=yourdomain.social
TAKAHE_EMAIL_SERVER=smtp://user:pass@host:port/
TAKAHE_EMAIL_FROM=admin@yoursite.social
TAKAHE_AUTO_ADMIN_EMAIL=you@gmail.com
TAKAHE_USE_PROXY_HEADERS=true
TAKAHE_ERROR_EMAILS=["you@gmail.com"]
TAKAHE_ENVIRONMENT=production

# This variable points to the google application credential file. It includes
# the project id, and as far as I can tell the documentation suggests that it
# should be all we need, but I couldn't get things working unless I included
# GCLOUD_PROJECT to explicitly state the project. Weird.
#
# Assumes the creds file is in a directory mounted at /creds
#
# https://cloud.google.com/docs/authentication/application-default-credentials
GOOGLE_APPLICATION_CREDENTIALS=/creds/application_default_credentials.json
GCLOUD_PROJECT=llimllib-takahe
```