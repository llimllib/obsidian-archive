https://www.reddit.com/r/golang/comments/6fl86p/wrapping_httpresponsewriter_for_middleware/dikqpag/

> tl;dr: ResponseWriter's optional interfaces spoil the fun, when you try to compose it in this (or any) way.

> The issue is, that the wrapping type now hides all the optional interfaces, `ResponseWriter` supports (namely [Flusher](https://godoc.org/net/http#Flusher), [Pusher](https://godoc.org/net/http#Pusher), [Hijacker](https://godoc.org/net/http#Hijacker) and [CloseNotifier](https://godoc.org/net/http#CloseNotifier).

> Even if the embedded `ResponseWriter` implements them, the type `statusRecorder` won't; it will only have the methods that are explicitly declared for it, plus the ones from embedded interfaces, that are known at compile time.

I hadn't considered the downisdes of wrapping ResponseWriter (which I've always done immediately) before.

Particularly, losing `Flusher` means losing the ability to [write chunked responses](https://stackoverflow.com/a/30603654/42559) which is [[The Weirdly Obscure Art of Streamed HTML|A really good way to have excellent performance]]