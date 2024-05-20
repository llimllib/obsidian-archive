---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
`gh api -H "Accept: application/vnd.github.raw+text" repos/<organization>/<repo>/contents/<file path and name>`

for example, to download [limbo's readme](https://github.com/llimllib/limbo/#readme):

`gh api -H "Accept: application/vnd.github.raw+text" repos/llimllib/limbo/contents/README.md`

If you don't include the `Accept` header, you'll get metadata about the file instead:

```json
$ gh api repos/llimllib/limbo/contents/README.md
{
  "name": "README.md",
  "path": "README.md",
  "sha": "f19cac71cafae51ae702da5f02c9be80a40cc2df",
  "size": 5374,
  "url": "https://api.github.com/repos/llimllib/limbo/contents/README.md?ref=master",
  "html_url": "https://github.com/llimllib/limbo/blob/master/README.md",
  "git_url": "https://api.github.com/repos/llimllib/limbo/git/blobs/f19cac71cafae51ae702da5f02c9be80a40cc2df",
  "download_url": "https://raw.githubusercontent.com/llimllib/limbo/master/README.md",
  "type": "file",
  "content": "IyBMaW1ibwoKIyMjIEEgW1NsYWNrXShodHRwczovL3NsYWNrLmNvbS8pIGNo\nYXRib3QKCiMjIFN0YXR1cwoKQXQgdGhlIG1vbWVudCwgSSBjb25zaWRlciBs\naW1ibyB0byBiZSBmZWF0dXJlIGNvbXBsZXRlLCBhbmQgdGhlIHByb2plY3Qg\naXMgaW4gbWFpbnRlbmFuY2UgbW9kZS4gRXZlcnkgb25jZSBpbiBhIHdoaWxl\nIEkgY29tZSBpbiBhbmQgdXBkYXRlIHRoZSBkZXBlbmRlbmNpZXMuCgpDb250\ncmlid>
  "encoding": "base64",
  "_links": {
    "self": "https://api.github.com/repos/llimllib/limbo/contents/README.md?ref=master",
    "git": "https://api.github.com/repos/llimllib/limbo/git/blobs/f19cac71cafae51ae702da5f02c9be80a40cc2df",
    "html": "https://github.com/llimllib/limbo/blob/master/README.md"
  }
}
```

the URLs of privately available files will include `token=` parameters allowing you to download them with, for example `wget $(gh api repos/organization/a_private_repo/contents/.secrets | jq -r .download_url)`