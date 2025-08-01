---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/a-h/templ

> A HTML templating language for Go that has great developer tooling.

You run a template generator as a pre-processor on your templates, and it turns them intoa go code.

The demo template looks like:

```html
package main

import "fmt"
import "time"

templ headerTemplate(name string) {
	<header data-testid="headerTemplate">
		<h1>{ name }</h1>
	</header>
}

templ footerTemplate() {
	<footer data-testid="footerTemplate">
		<div>&copy; { fmt.Sprintf("%d", time.Now().Year()) }</div>
	</footer>
}

templ navTemplate() {
	<nav data-testid="navTemplate">
		<ul>
			<li><a href="/">Home</a></li>
			<li><a href="/posts">Posts</a></li>
		</ul>
	</nav>
}

templ layout(name string, content templ.Component) {
	<html>
		<head><title>{ name }</title></head>
		<body>
			{! headerTemplate(name) }
			{! navTemplate() }
			<main>
				{! content }
			</main>
		</body>
		{! footerTemplate() }
	</html>
}

templ homeTemplate() {
	<div data-testid="homeTemplate">Welcome to my website.</div>
}

templ postsTemplate(posts []Post) {
	<div data-testid="postsTemplate">
		for _, p := range posts {
			<div data-testid="postsTemplatePost">
				<div data-testid="postsTemplatePostName">{ p.Name }</div>
				<div data-testid="postsTemplatePostAuthor">{ p.Author }</div>
			</div>
		}
	</div>
}

templ home() {
	{! layout("Home", homeTemplate()) }
}

templ posts(posts []Post) {
	{! layout("Posts", postsTemplate(posts)) }
}
```