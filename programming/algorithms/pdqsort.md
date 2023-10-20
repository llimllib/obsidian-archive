https://github.com/orlp/pdqsort

> Pattern-defeating quicksort (pdqsort) is a novel sorting algorithm that combines the fast average case of randomized quicksort with the fast worst case of heapsort, while achieving linear time on inputs with certain patterns. pdqsort is an extension and improvement of David Mussers introsort. All code is available for free under the zlib license.

noticed it because [go will be using it](https://github.com/golang/go/commit/72e77a7f41bbf45d466119444307fd3ae996e257) in the next release. Note that this makes the default sort unstable! It was previously not guaranteed to be stable, but was in practice

[news.yc comments here](https://news.ycombinator.com/item?id=31106157) 

[here's a youtube talk](https://www.youtube.com/watch?v=jz-PBiWwNjc) from the author that I have not watched