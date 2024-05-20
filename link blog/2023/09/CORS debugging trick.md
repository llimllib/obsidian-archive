---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
a CORS error throws a `securitypolicyviolation` event. This would have saved me some time debugging in the past if I knew it!

```javascript
document.body.addEventListener(  
	"securitypolicyviolation",  
	(e) => { console.log(e) }  
)
```

via [this toot](https://fosstodon.org/@VincentTunru/110983667693083297) by Vincent Tunru