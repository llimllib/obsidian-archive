---
created: 2024-06-10T15:11:35.750Z
updated: 2024-06-10T15:11:35.750Z
---
> A minimal Slack clone built with Elixir & Phoenix LiveView

very young, but might be similar to what I was thinking with [[Elixir chat server]]

via github front page, a friend starred it.

To setup, using [[mise]]; I had not previously installed erlang or elixir on this computer:

```
mise use elixir
mise use erlang
mix setup
```

That ended up with postgres errors. I took a detour to install [[elixir-ls]], then edited `config/dev.exs` to change `postgres` to my username.

After that, `mix setup` worked and I could start the server with `mix phx.server`

- I was able to register a user
- I then entered a message in the chat
- the app threw me to an error page about no route for `POST /`