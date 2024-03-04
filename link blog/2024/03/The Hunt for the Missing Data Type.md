https://www.hillelwayne.com/post/graph-types/

> There is almost no graph support in any mainstream language. None have it as a built-in type, very few have them in the standard library, and many don’t have a robust third-party library in the ecosystem. Most of the time, I have to roll graphs from scratch. There’s a gap between how often software engineers could use graphs and how little our programming ecosystems support them. Where are all the graph types?

...

> Many, many graph algorithms are NP-complete or harder. While NP-complete is often tractable for large problems, graphs can be _enormous_ problems. The choice of representation plays a big role in how fast you can complete it, as do the specifics of your algorithm implementation...

> All of this means that if you have graph problems you want to solve, you need a lot of control over the specifics of your data representation and algorithm. You simply cannot afford to leave performance on the table.

> So, the reasons we don’t have widespread graph support:

> - There are many different kinds of graphs
> - There are many different representations of each kind of graph
> - There are many different graph algorithms
> - Graph algorithm performance is very sensitive to graph representation and implementation details
> - People run very expensive algorithms on very big graphs.

via [news.yc](https://news.ycombinator.com/item?id=39592444)

