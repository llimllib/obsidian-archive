---
created: 2024-10-10T14:24:17.784Z
updated: 2024-10-10T14:24:17.784Z
---
https://developer.mozilla.org/en-US/docs/Web/URI/Fragment/Text_fragments

You can append `#:~:text=bananas` to a URL to highlight the first match of the text `bananas` on the page that's linked. You can append `#:~:text=initio,finito` to highlight all text in the first match from `initio` to `finito`.

For example, [this link](https://notes.billmill.org/link_blog/2024/10/No__really_-_YAGNI.html#:~:text=You%20can't,no%20one%20can)  with `#:~:text=You can't,no one can` highlights the phrase `You can't predict the future, no one can` on the linked page.

The browser will scroll the page to the first instance of the fragment text. [This link](https://www.gutenberg.org/cache/epub/64317/pg64317-images.html#:~:text=so%20we%20beat%20on,past) should take you right to the famous final line of The Great Gatsby.

I'm very excited to use this feature! I wish it'd been around for a long time.