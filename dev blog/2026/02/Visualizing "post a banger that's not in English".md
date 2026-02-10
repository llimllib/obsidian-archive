---
created: 2026-02-10T02:15:03.934Z
updated: 2026-02-10T02:15:03.934Z
---
https://llimllib.github.io/banger_crawler
https://github.com/llimllib/banger_crawler

There's been a thread on bsky lately where people post a song link and the text "post a banger that's not in English". 

The bsky UI makes it pretty hard to navigate the tree of "skeets" and "quote skeets" (I still can't say these phrases seriously...) which got me wondering what the tree of posts actually looks like.

Here's the visualization the LLM gave me, with only minor editing. It reads from the center outwards, and reveals that the first post was (humorously)  Scatman John's "Scatman (ski-ba-bop-da-ba-bop)":

![[Pasted image 20260209212144.png]]

If you go to [the site](https://llimllib.github.io/banger_crawler), can click on a post to play the song that's referenced.

There's a full database in the [source](https://github.com/llimllib/banger_crawler), the most common songs referenced are (to a rough estimation):

| #   | Song                                          | Posts |
| --- | --------------------------------------------- | ----- |
| 1   | [Adriano Celentano - Prisencolinensinainciusol](https://www.youtube.com/watch?v=fU-wH8SrFro) | 48    |
| 2   | [Plastic Bertrand - Ça Plane Pour Moi](https://www.youtube.com/watch?v=Ln31raI2ezY)          | 24    |
| 3   | [Nena - 99 Luftballons](https://www.youtube.com/watch?v=Fpu5a0Bl8eY)                         | 17    |
| 4   | [La Bamba](https://www.youtube.com/watch?v=BycLmWI97Nc)                                      | 12    |
| 5   | [O-Zone - Dragostea Din Tei](https://www.youtube.com/watch?v=YnopHCL1Jk8)                    | 11    |
| 6   | [The HU - Wolf Totem](https://www.youtube.com/watch?v=jM8dCGIm6yc)                           | 9     |
| 7   | [Rammstein - Du Hast](https://www.youtube.com/watch?v=W3q8Od5qJio)                           | 8     |
| 8   | [Falco - Der Kommissar](https://www.youtube.com/watch?v=8-bgiiTxhzM)                         | 8     |
| 9   | [The HU - Yuve Yuve Yu](https://www.youtube.com/watch?v=v4xZUr0BEfE)                         | 7     |
| 10  | [Stromae - Papaoutai](https://www.youtube.com/watch?v=oiKj0Z_Xnjc)                           | 7     |

There's a duckdb file in the repository so you can run your own queries if you'd like.

On bluesky, I talked a bit about the difference that the LLM makes to this sort of tiny project, I was able to churn it out in a half hour while chatting with my kids, whereas in the past I definitely would have said "oh that's a neat idea", and then done nothing with it.
