> This program generates bitmaps that are locally similar to the input bitmap.

[![main collage](https://github.com/mxgmn/WaveFunctionCollapse/raw/master/images/wfc.png)](https://github.com/mxgmn/WaveFunctionCollapse/blob/master/images/wfc.png)

Implemented in many languages. [video demonstration](https://youtu.be/DOQTr2Xmlz0)

> WFC initializes output bitmap in a completely unobserved state, where each pixel value is in superposition of colors of the input bitmap (so if the input was black & white then the unobserved states are shown in different shades of grey). The coefficients in these superpositions are real numbers, not complex numbers, so it doesn't do the actual quantum mechanics, but it was inspired by QM. Then the program goes into the observation-propagation cycle:

> -   On each observation step an NxN region is chosen among the unobserved which has the lowest Shannon entropy. This region's state then collapses into a definite state according to its coefficients and the distribution of NxN patterns in the input.
> -   On each propagation step new information gained from the collapse on the previous step propagates through the output.


Found via [untangle](https://www.inkandswitch.com/untangle/) blog post