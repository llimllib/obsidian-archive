The atuin docs for self-hosting are [very skimpy](https://atuin.sh/docs/self-hosting/)

Here's how I self-hosted an [[atuin]] server:

1. Make `~/srv/atuin`
2. Copy the docker-compose.yml file from [here](https://github.com/atuinsh/atuin/blob/main/docker-compose.yml) to `~/srv/atuin/docker-compose.yml`
3. Changes I made to that file:
	1. change the host port from `8888` to `12321` (the host port is the first number, so `12321:8888`. I forget the order of these every single time)
	2. update the password from `really-insecure` to a random string
	3. change `restart: always` to `restart: unless-stopped`; this is the same except it allows you to stop it, which is probably what you want
4. start the server: `docker compose up -d`
5. Now you should have a running server! The next step is to create an account. From one client computer:
	1. edit `~/.config/atuin/config.toml` (that's where it lives on my system anyway, find your config file). Uncomment `sync_address` and change it to `http://<your-host>:12321`
		1. I did not bother to enable TLS on my server because I'm not going to expose it outside of my home network; if you do, use `https` instead of `http`
	2. run `atuin account register`
		1. follow the prompts to create a user, and save your password to your password manager
	3. run `atuin key` and store the output to your password manager
6. Now you have a user on the server. For each client computer:
	1. update `sync_address` in your config file
	2. run `atuin login`
		1. Make sure you give it the encryption key you got from `atuin key`
	3. run `atuin sync`