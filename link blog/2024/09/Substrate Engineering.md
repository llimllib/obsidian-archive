---
created: 2024-09-11T13:25:22.383Z
updated: 2024-09-11T13:25:22.383Z
---
> Writing code is much, much easier than reading code later and understanding it, still less spotting bugs in it. Spotting a bug is a challenge even when you know there is a bug: that’s what debugging is, and it’s hard. And when you prompt Copilot or Cody, and use the code it provides, code review is exactly what we are doing.

> The _better_ LLMS get -
>      the _more_ they **boost velocity**
>      by generating **working code** -
> the _harder_ it will be to notice when
>      they get things **wrong**

> Our software foundations need to get much better, across the board, or else widespread use of LLMs is going to make our software quality much worse. Our only chance is to double down on defense in depth: in making all of our software foundations better.

- [Chris Krycho](https://v5.chriskrycho.com/elsewhere/substrate-engineering/)

Goes on to talk about designing configuration languages that are more robust to LLM's imaginations and mentions [[Dhall]] and [[Starlark]]

> if we take this space seriously — and we should! — I think there is room to build a language that has a lot of what Starlark has going for it in terms of familiarity and accessibility, but which also pulls in the good ideas from Dhall’s type system. And then we could see: does it work well? Where does it fall down? And does it in fact help with providing useful guardrails for using LLMs? I don’t know: it’s a hypothesis. But we should try it!