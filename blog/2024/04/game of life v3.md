---
updated: '2024-04-20T17:18:15Z'
created: '2024-04-20T16:46:42Z'
---
https://llimllib.github.io/ca/03/

My kids inexplicably wanted to play the quick game of life I coded a year ago.

Unfortunately when I opened it up and tried to use it, performance had regressed in firefox tremendously - it was unusably slow.

So I profiled it, and found that drawing rectangles to a canvas in firefox seems to be a lot slower than in safari. With that in mind, I figured out how to [draw cells to the canvas using `putImageData`](https://github.com/llimllib/ca/blob/be2aa7c4180623fe78f03d7f0a1ea49530d6fb85/03/index.js#L72-L85), which sped the program up nicely.

```js
drawCells() {
	const data = this.ctx.createImageData(this.width, this.height);
	// data.buffer is a Uint8Array by default. You can either edit the
	// array as 4 bytes per pixel, or interpret it as a single 4-byte
	// integer. The latter is more convenient here.
	const buf = new Uint32Array(data.data.buffer);
	//              A B G R
	const alive = 0xffc038fa;
	const dead = 0xfffa5f38;
	let i = 0;
	for (let y = 0; y < this.height; y++) {
		for (let x = 0; x < this.width; x++) {
			// convert from screen coords into automata coords
			const cellx = Math.floor(x / this.cellsize);
			const celly = Math.floor(y / this.cellsize);
			buf[i++] = this.cells[celly * this.cols + cellx] ? alive : dead;
		}
	}
	this.ctx.putImageData(data, 0, 0);
}
```