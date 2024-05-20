---
updated: '2024-04-03T02:51:19Z'
created: '2024-03-17T14:46:44Z'
---
_update apr 2_: I accidentally deleted this article and now have re-posted it

in [[What are the "worst" spelling bee pangrams?|part 1]], I introduced the spelling bee and the concept of the "worst" pangram, which I defined as the one which produced the fewest possible words. Then I wrote and described a program that found them, and labelled `equivoke` the Worst Pangram™.

I thought I was done getting nerdsniped after that, but a few people helpfully provided bits of information I was missing the first time, and I also thought a bit more about the problem to change its definition a bit.

## more better information

People shared two bits of information with me that I didn't have when I started:

- On mastodon, Brad Greenlee [shared](https://fiasco.social/@brad/112108107787262025) [a wordlist](https://github.com/bgreenlee/spelling-beat/blob/main/js/application.js#L4) he's been working on for his spelling bee solver. This pared-down scrabble wordlist is much closer to what a real spelling bee word list looks like
- On reddit, `cearrach` informed me that a Genius score is 70% of the total points for a puzzle.

I took Brad's word list (thanks!) and added calculation of the word score and each pangram's total score. I didn't mention how words are scored in the first article:

- a 4 letter word is worth 1 point
- any word with more than 4 letters is worth as many points as it has letters
- a pangram scores a 7 point bonus

This led to a funny result, where `fuckwit` was the new "worst" pangram:

![[Pasted image 20240317091610.png]]

## back to the beginning

The initial prompt for this exploration was a question about whether there were any spelling bee puzzles where just the pangram would get you to the "genius" level.

I had changed the question to suit the knowledge I had at the start, but now I realized I had enough information to try and answer the original question.

I looked at that list and realized that if you set the puzzle as `jacquard`, and used the `q` as a required letter, you'd have only the pangram and three additional words: `aqua`, `qajaq` (an alternative spelling of `kayak`, apparently!) and `quad`. That would give you:

- `jacquard`: 7 + 8 = 15 points
- `aqua`: 1
- `qajaq`: 5
- `quad`: 1

So `jacQuard` would result in a puzzle where the pangram was responsible for 15/22 points, or just a tiny hair below genius level. Could we do better?

I took the same program I used in part 1 and added a search through each letter of the pangram, scoring the result of making that letter required.

Here's a table of every pangram my program finds that would reach genius level all by itself:

| score | pangram          | words                         |
| ----- | ---------------- | ----------------------------- |
| 14    | mitz**v**ah      |                               |
| 14    | princo**x**      |                               |
| 15    | **v**agotomy     |                               |
| 15    | **v**iburnum     |                               |
| 15    | conflu**x**      | flux                          |
| 15    | jukebo**x**      | jeux                          |
| 15    | ca**z**ique      | quiz                          |
| 15    | ga**z**pacho     |                               |
| 16    | bo**v**inity     | viny                          |
| 16    | checkbo**x**     | exec                          |
| 16    | fo**x**hound     | doxx                          |
| 16    | qui**x**ote      | exit,text                     |
| 17    | b**i**keway      | bike,kiwi,wiki                |
| 17    | **j**udicial     | jail,juju                     |
| 17    | e**x**iguity     | exit,text                     |
| 17    | tubife**x**      | exit,ibex,text                |
| 17    | activi**z**e     | zeta,ziti                     |
| 18    | ja**c**quard     | card,crud,curd                |
| 18    | hi**g**hjack     | gaga,high,jagg                |
| 18    | bull**w**hip     | whip,whup,will                |
| 18    | o**x**azepam     | apex,exam,expo                |
| 19    | **g**azpacho     | agog,gaga,goop,pogo           |
| 19    | **p**uffbird     | burp,drip,puff,purr           |
| 19    | exiguit**y**     | eggy,itty,yegg,yeti           |
| 19    | bu**zz**word     | bozo,buzz,orzo,ouzo           |
| 19    | **z**ucchetto    | chez,ooze,ouzo                |
| 20    | mitz**v**oth     | vomit                         |
| 20    | **v**anguard     | guava                         |
| 20    | duck**w**alk     | claw,wack,walk,wall,waul      |
| 20    | ki**w**ifruit    | kiwi,twit,wiki,writ           |
| 20    | qui**x**otic     | toxic                         |
| 21    | **b**ijective    | beet,bite,jibb,jibe,vibe      |
| 21    | cheap**j**ack    | hajj,jack,jake,jape,jeep      |
| 21    | equivo**k**e     | evoke,kook                    |
| 21    | jacq**u**ard     | aqua,aura,crud,curd,juju,quad |
| 21    | **v**ibraharp    | brava                         |
| 21    | bo**x**thorn     | hotbox                        |
| 21    | py**x**idium     | mixup,pixy                    |
| 22    | tubi**f**icid    | biff,buff,cuff,duff,tiff,tuft |
| 22    | exempti**v**e    | peeve,veep                    |
| 22    | i**v**orybill    | ivory,viol                    |
| 22    | phototo**x**ic   | toxic                         |
| 23    | to**x**icologic  | toxic                         |
| 24    | epexe**g**etic   | epigeic                       |
| 25    | a**q**uacultural | aqua,quart                    |

## implementation

Following the same start of the program I used to find the word count for every pangram in [[What are the "worst" spelling bee pangrams?|part 1]], I added a couple more loops:

- let $scoresWithReqLetters$ be a list of tuples ($totalScore$, $requiredLetter$, $pangram$)
- For each pangram
  - find all words that match the pangram
  - for each letter in the pangram
    - sum the score of each word that contains the letter
    - add that score, the letter, and the pangram to $scoresWithReqLetters$
- Sort $scoresWithReqLetters$
- For each pangram
  - if the score of the pangram is > 70% of $totalScore$, print it out

The implementation in python:

```python
@cache
def wscore(w):
    return (1 if len(w) == 4 else len(w)) + (7 if len(allwordsets[w]) == 7 else 0)


# find all matches for each pangram, then the score for each possible required
# letter
scores_with_req_letters = []
pangram_matches = {}
for points, _, pangram in pangrams:
    ps = allwordsets[pangram]
    matches = [w for w in allwords if allwordsets[w].issubset(ps) and w != pangram]
    for l in ps:
        lmatches = [m for m in matches if l in m]
        pangram_matches[(pangram, l)] = lmatches
        score = len(pangram) + 7 + sum(wscore(m) for m in lmatches)
        scores_with_req_letters.append((score, l, pangram))


@cache
def hl(w: str, l: str) -> str:
    return f"{red}{w.replace(l, f'{yellow}{l}{red}')}"


red = "\N{esc}[0;31m"
green = "\N{esc}[0;32m"
yellow = "\N{esc}[0;33m"
blue = "\N{esc}[0;34m"
reset = "\N{esc}[0m"
print(f"{green}points\tpangram\t\twords")
scores_with_req_letters.sort()
for points, l, pangram in scores_with_req_letters:
    matches = pangram_matches[(pangram, l)]
    panscore = wscore(pangram)
    total = panscore + sum(wscore(m) for m in matches)
    if (panscore / total) > 0.7:
        matchstr = ",".join(matches)
        if len(matchstr) > 60:
            matchstr = matchstr[:59] + "..."
        print(
            f"{blue}{points: <8}{hl(pangram, l)}{' ' * (16-len(pangram))}{reset}{matchstr}"
        )
```

I didn't dive much into performance, but here's a few notes:

- pypy runs this program quite a bit faster than cpython on my machine, roughly 46s to 77s
- The program spends almost all its time finding every matching word for every pangram, if I were to speed it up that would be the loop I would target
- Caching the construction of all sets at the beginning of the run was a simple and significant performance win

With that, I feel like I can finally wash my hands of this problem! (Maybe? we'll see!)
