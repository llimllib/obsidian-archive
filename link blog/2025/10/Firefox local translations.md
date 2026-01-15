---
created: 2025-10-31T14:22:24.713Z
updated: 2025-10-31T14:22:24.713Z
---
I discovered this morning via [mastodon](https://metasocial.com/@trs/115467075855938295) that Firefox has a local translation model, accessible via `about:translations`. This is very neat!

So I wanted to see if I could get it working via the command line, and did a bit of digging.

The [Firefox source code for it is here](https://github.com/mozilla-firefox/firefox/tree/50445a0ee5bbeaeba68911b649963669e4c483e2/toolkit/components/translations), it uses [CLD2](https://github.com/CLD2Owners/cld2) as a language detector, and then [marian](https://marian-nmt.github.io/) to do the actual translation.

They have a nice [documentation page](https://firefox-source-docs.mozilla.org/toolkit/components/translations/resources/01_overview.html) for it.

Unfortunately, so far I didn't find a way to use it from the command line, and I also failed to build marian for my mac.