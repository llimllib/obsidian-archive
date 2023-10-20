https://supabase.com/blog/edge-runtime-self-hosted-deno-functions

> Supabase Edge Runtime is a web server written in Rust that uses a custom Deno runtime. It can serve TypeScript, JavaScript, and WASM functions. All your existing Edge Functions run on Edge Runtime without changing a single line of code.

> ...Self-hosting is not the only benefit of Edge Runtime. It will improve the local development experience of Edge Functions.

> Supabase CLI can now serve all local Edge Functions by running `supabase functions serve`. Previously, you could only serve a single Edge Function at a time. This was not a great experience for local development. Some of you even devised [clever hacks](https://github.com/orgs/supabase/discussions/6786) to get around this limitation.