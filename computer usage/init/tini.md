https://github.com/krallin/tini

> Tini is the simplest `init` you could think of.

> All Tini does is spawn a single child (Tini is meant to be run in a container), and wait for it to exit all the while reaping zombies and performing signal forwarding.

I found this via [this dockerfile for cronicle](https://github.com/bluet/docker-cronicle-docker), a neat spin on init