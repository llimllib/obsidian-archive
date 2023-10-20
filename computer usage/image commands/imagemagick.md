Convert a png to jpg, resize it, and optimize it for display on a website:

```
convert image.png -resize 300x300 -strip -interlace Plane -quality 75% public/static/headshot.jpg
```

Use the `identify` program to display information about an image (or a set of images):

```
$ identify public/static/headshot.jpg
public/static/headshot.jpg JPEG 300x300 300x300+0+0 8-bit sRGB 21937B 0.000u 0:00.000
```

concatenate two images vertically:

```
convert -append image1.png image2.png vertical_both.png
```

horizontally:

```
convert +append image1.png image2.png horizontal_both.png
```