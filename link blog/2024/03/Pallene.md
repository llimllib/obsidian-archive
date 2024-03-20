https://www.inf.puc-rio.br/~roberto/docs/Gualandi-2020-SCP.pdf

> With the insight that programmers are willing to restrict their use of dynamic language features when performance matters, we have decided to explore a return to the traditional scripting architecture through Pallene, a system programming language that we have designed specifically to complement Lua. Since Pallene has static types, it can obtain good performance with an ahead-of-time compiler, avoiding the complexities of just-in-time compilation; and since it is designed specifically to be used with Lua, we hope Pallene will be attractive in situations where using C would be too cumbersome.

> Overall, our goals for Pallene are that it should be safe, predictably efficient, seamlessly interoperable with Lua, and easy for Lua programmers to learn. Furthermore, it should have a simple and maintainable implementation that is as portable as Lua itself.  achieve these goals, we designed Pallene as an ahead-of-time-compiled, typed subset of Lua, which can directly manipulate Lua data structures, which shares Lua’s runtime and garbage collector...

> Inspired by optional and gradual typing, Pallene is very close to a typed subset of Lua

https://github.com/pallene-lang/pallene , looks like development may be paused

via [@akkartik](https://merveilles.town/@akkartik/112129169585720317)