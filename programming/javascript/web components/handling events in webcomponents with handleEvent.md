---
created: 2024-10-01T18:05:18.651Z
updated: 2024-10-01T18:05:18.651Z
---
https://gomakethings.com/the-handleevent-method-is-the-absolute-best-way-to-handle-events-in-web-components/

basically, this:

```javascript
customElements.define('awesome-sauce', class extends HTMLElement {

	// Instantiate the component
	constructor () {
		super();
	}

	// Handle events
	handleEvent (event) {
		// ...
	}

	// Listen for events
	connectedCallback () {
		this.addEventListener('click', this);
		this.addEventListener('input', this);
		this.addEventListener('close', this);
	}

});
```