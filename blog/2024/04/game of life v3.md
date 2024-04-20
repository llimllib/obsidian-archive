https://llimllib.github.io/ca/03/

My kids inexplicably wanted to play the quick game of life I coded a year ago.

Unfortunately when I opened it up and tried to use it, performance had regressed in firefox tremendously - it was unusably slow.

So I profiled it, and found that drawing rectangles to a canvas in firefox seems to be a lot slower than in safari. With that in mind, I figured out how to [draw cells to the canvas using `putImageData`](https://github.com/llimllib/ca/blob/be2aa7c4180623fe78f03d7f0a1ea49530d6fb85/03/index.js#L72-L85), which sped the program up nicely.