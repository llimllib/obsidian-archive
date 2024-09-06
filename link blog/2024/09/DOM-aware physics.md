---
created: 2024-09-06T13:00:02.884Z
updated: 2024-09-06T13:00:02.884Z
---
https://threadreaderapp.com/thread/1831783365483360539.html

Elad Bezalel walks through how they implemented falling blocks that bounce off DOM elements:

- apply CSS filters to increase contrast
- snapshot the page with [modern-screenshot](https://github.com/qq15725/modern-screenshot)
	- includes a plug for this library as particularly excellent. 
	- I currently use d3-svg-to-png in [nbastats](https://github.com/llimllib/nbastats), I should give modern-screenshot a try
- trace the dom with [this WASM version of Potrace](https://github.com/tomayac/esm-potrace-wasm)
- use [matter.js](https://brm.io/matter-js/) for the rigid-body physics