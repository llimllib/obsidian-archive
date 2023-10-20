https://dev.to/tigt/the-weirdly-obscure-art-of-streamed-html-4gc2

Part 2 of an excellent series on rebuilding an ecommerce website to be as fast as humanly possible (while accepting mostly normal constraints)

mentions streaming HTML, which was not a technique I was familiar with and after reading the post I still don't _thoroughly_ understand.

Mentions [[marko]] as a templating language that can make particular use of streaming:

> Marko streams HTML with [its `<await>` tag](https://markojs.com/docs/core-tags/#await). I was pleasantly surprised at how easily it could optimize browser rendering, with all the control I wanted over HTTP, HTML, and JavaScript...
> 
> Imagine a component that displays recommended products. Fetching the recommendations is usually fast, but every once in a while, the API hiccups. `<await>`’s got your back:  

```
<await(productRecommendations)
    timeout=50> <!-- wait up to 50ms -->
  <@then|recs|>
    <RecommendedProductList of=recs />
  </@then>

  <@catch>
    <!-- don’t render anything; no big deal if this fails -->
  </@catch>
</await>
```

then, you can add `client-reorder`:

> The `client-reorder` attribute turns the `<await>` into an HTML fragment that doesn’t delay the rest of the page behind it, but asynchronously renders when ready. `client-reorder` requires JavaScript, so you can weigh the tradeoffs of using it vs. a `timeout` with no fallback. (I think you can even combine them.)

-----

The best resource I can find on sending HTTP streaming requests in Go seems to be [this stackoverflow post](https://stackoverflow.com/a/30603654/42559)? Surely there must be better.