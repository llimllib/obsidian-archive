---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://www.gnu.org/software/wget/

Here's an example command I used recently to download all music files from a webpage:

```
 wget --no-parent --recursive --level=1 --no-directories \
   'https://gdarchive.net/Public/Bluegrass/Artists%20A%20-%20K/Bela%20Fleck%20&%20Chris%20Thile/bf+ct2016-07-19.cmc-8.audfellow.flac16/'
 ```