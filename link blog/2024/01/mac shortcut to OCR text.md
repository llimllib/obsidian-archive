---
updated: '2024-01-02T21:02:11Z'
created: '2024-01-02T20:56:12Z'
---
https://blog.greg.technology/2024/01/02/how-do-you-ocr-on-a-mac.html

Guides you through using the `Shorcuts` app to create a command-line interface to Mac OS X's OCR engine, via `shortcuts run ocr-text -i <image file>`.

I tested it out and it works! Very cool. Too bad that none of the [[mac os command line programs]] provide this natively, it would be very useful to provide system functionality without requiring a shortcut.

![[Pasted image 20240102155842.png]]
It copies the text of the image to the clipboard by default, but you can get it to output it to the command line by piping to `cat`: `shortcuts run ocr-text -i <image file> | cat`