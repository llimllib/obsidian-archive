---
updated: '2024-04-20T19:09:08Z'
created: '2024-04-20T16:46:42Z'
---
- neat square wave function: `y = ceil(sin(x+u_time)) + floor(sin(x+u_time));`, I'd never considered it in that way before
- Golan Levin's shaping functions:
	- [polynomial](http://www.flong.com/archive/texts/code/shapers_poly/)
	- [exponential](http://www.flong.com/archive/texts/code/shapers_exp/)
	- [elliptical](http://www.flong.com/archive/texts/code/shapers_circ/)
	- [bezier + other](http://www.flong.com/archive/texts/code/shapers_bez/)
- Inigo Quilez has many resources, but [here is one of shaping functions](https://iquilezles.org/articles/functions/)
	- each one is also available in the very cool [graphtoy.com](https://graphtoy.com/)
		- sadly can't seem to link directly to functions because the unescaped parens mess up the markdown formatting. Maybe they could be escaped, but, irritating.
- [lygia.xyz](https://lygia.xyz) shader library