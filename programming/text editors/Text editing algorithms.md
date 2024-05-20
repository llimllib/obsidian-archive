---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Nice article from jetbrains on the data structures in use in their new editor; ropes and interval trees particularly:

https://blog.jetbrains.com/fleet/2022/02/fleet-below-deck-part-ii-breaking-down-the-editor/

Mentions the Rope Science course from Raph Linus: 

https://abishov.com/xi-editor/docs/rope_science_00.html

who says on hn:

> I'm happy to see them cite my Rope Science series. Looking back, there were some things that xi did wrong, most importantly separating the front-end from the back-end with async communication, but the data structures and text manipulation algorithms were solid.

the hn comments mention several times _piece tables_, from "Data Structures for Text Sequences" by Crowley 1998

https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.48.1265&rep=rep1&type=pdf

> The data structure used to maintain the sequence of characters is an important part of a text editor. This paper investigates and evaluates the range of possible data structures for text sequences. The ADT interface to the text sequence component of a text editor is examined. Six common sequence data structures (array, gap, list, line pointers, fixed size buffers and piece tables) are examined and then a general model of sequence data structures that encompasses all six structures is presented. The piece table method is explained in detail and its advantages are presented. The design space of sequence data structures is examined and several variations on the ones listed above are presented. These sequence data structures are compared experimentally and evaluated based on a number of criteria. The experimental comparison is done by implementing each data structure in an editing simulator and testing it using a synthetic load of many thousands of edits.

This article talks about the reasoning for the move from a _line array_ to a piece table in VS code:

https://code.visualstudio.com/blogs/2018/03/23/text-buffer-reimplementation

