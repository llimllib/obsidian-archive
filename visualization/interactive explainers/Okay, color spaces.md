https://ericportis.com/posts/2024/okay-color-spaces/

Lovely 3d interactive visualizations of color spaces, in this case with a responsive 2d slice of the color space displayed beside it

![[Pasted image 20240221103330.png]]

---

> The first attempt at “it” (a perceptually-uniform color space) was made by [Albert Munsell](https://en.wikipedia.org/wiki/Albert_Henry_Munsell), who [described his space in 1905](https://www.gutenberg.org/files/26054/26054-h/26054-h.htm#tag5) (charmingly, as a “COLOR TREE”) and [published an “Atlas” to it in 1913](https://library.si.edu/digital-library/book/atlasmunsellcol00muns).

> The central “trunk” of Munsell’s TREE goes from black at the bottom, through grey in the middle, to white at the top. The middle expands outwards into a rainbow of “branches”, with each angle around the trunk representing a particular hue. Each branch starts off desaturated near the middle, and gets more and more saturated the further out it goes.

![[Pasted image 20240221103724.png]]

---

> But – tragically! – [CIELAB isn’t exactly perceptually uniform](https://www.w3.org/Graphics/Color/Workshop/slides/talk/lilley#limit). Worse, the more experiments people did, the clearer it became that _no_ three-dimensional space _could ever_ be perceptually uniform; three dimensions just cannot capture all of the weird and wonderful ways that our eyes and brains process color comparisons.

---

> Thankfully – turns out! – Oklab was explicitly designed so that movement up/down, in/out, and around the L axis works exactly like navigating Munsell’s COLOR TREE. Each type of movement changes _just one, psychologically-independent thing_: the lightness, chroma, or hue of the color. In order to navigate Oklab like this, we need to use a polar coordinate system, instead of a rectangular one. When we do, we refer to the space by another name: `OKLCH`

---

![[Pasted image 20240221104210.png]]

