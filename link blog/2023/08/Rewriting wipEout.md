https://phoboslab.org/log/2023/08/rewriting-wipeout
https://github.com/phoboslab/wipeout-rewrite

The author of the post took the leaked source code of the game "wipEout", a launch title for the Playstation, and refactored it far enough that they call it a rewrite.

The post is an excellent overview of the author's work and how they though about each step.

> The quality of the leaked source is abysmal...
> Let me paint you a picture: Even the NTSC version for the PlayStation looks like an afterthought quickly hacked into the PAL version. #ifdefs switched some physics calculations from 25 fps to 30. Later, the PC DOS release, Win95 version and finally the ATI Rage Edition were haphazardly piled on top. Each time by a different set of developers that somehow had to make sense of this mess. The code still contains many of the remains of what came before. There was never any time to clean it up.

---

> The PSX devkits came with a library called LIBGPU, which handled the rendering. Since the PSX GPU didn't have a z-buffer, all primitives you wanted to draw (triangles, quads and sprites) needed to be submitted into an “ordering table” or OT for short. This table had (typically) 8192 slots allowing for 8192 different z-levels. The GPU would then rasterize the list back to front. The result would not be perfect (in some situations neither of two polygons will have all pixels in front of the other one), but close enough.

> The ordering table necessitates that you know the z-depth of each primitive before you hand it to the GPU for drawing. It is my understanding that the PSX original did the perspective calculations on a co-processor...

I'm going to try not to quote the _entire_ article, so I recommend you go read it if nerdery like this is interesting to you.

Via [this toot](https://floss.social/@pieq/110874428576044562)