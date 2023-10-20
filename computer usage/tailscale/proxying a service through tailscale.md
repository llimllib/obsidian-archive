1. Start up a service serving traffic locally on a port - I started up [elk](https://github.com/elk-zone/elk) on port 5314
2. [Install tailscale](https://tailscale.com/download/linux/ubuntu-2204) on the server
	1. including sign into the tailnet
3. proxy via caddy

```
elk.example.com {
	handle {
		reverse_proxy <local_host_name>:5314
	}
}
```

and that's it! super easy, very impressive