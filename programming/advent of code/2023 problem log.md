**WARNING**: spoilers ahead!

- [[2023 problem log#Day 1|day 1]]
- [[2023 problem log#Day 2|day 2]]
- [[2023 problem log#Day 3|day 3]]
- [[2023 problem log#Day 4|day 4]]
- [[2023 problem log#Day 5|day 5]]
- [[2023 problem log#Day 6|day 6]]
## Day 1

Tougher than a usual day 1! The second part in particular requires you to either find overlapping matches (`1twone` -> `[1, two, one]`) or to search from the end to the front.

I solved it by detecting overlapping matches with a neat regular expression trick: a lookahead capture group. The key idea is that if you put a capture group inside a lookahead group (denoted by `(?= )`), you'll get a match but won't consume any of the string; this allows you to find overlapping matches.

```python
>>> import re

>>> re.findall("(?=(\d|two|one))", "1twone")
['1', 'two', 'one']
```

- [day 1 problem](https://adventofcode.com/2023/day/1)
- [my day 1 answer](https://github.com/llimllib/personal_code/blob/47a3aa22865fa5a52f04d11d845991f6612b2508/misc/advent/2023/01/a.py)

## Day 2

A nice easy start-of-season problem today. First I solved it the straightforward way, by parsing the file into a dictionary of lists, then iterating through each game in the dictionary.

Afterwards, I realized that all you need is the maximum red, green and blue values from each line; so I wrote a little function to pull out one color's maximum with a regular expression:

```python
def maxi(line, color):
    return max(int(x) for x in re.findall(rf"(\d+) {color}", line))
```

And then the solutions basically just fall out as two generator expressions:

```python
print(
    sum(
        i + 1
        for i, line in enumerate(open("input.txt"))
        if maxi(line, "red") <= 12
        and maxi(line, "green") <= 13
        and maxi(line, "blue") <= 14
    )
)

print(
    sum(
        maxi(line, "red") * maxi(line, "blue") * maxi(line, "green")
        for line in open("input.txt")
    )
)
```

- [day 2 problem](https://adventofcode.com/2023/day/2)
- [straightforward answer](https://github.com/llimllib/personal_code/blob/08a22e4f01797acaab704a5f331a4e067e65b86a/misc/advent/2023/02/a.py)
- [little bit more clever answer](https://github.com/llimllib/personal_code/blob/08a22e4f01797acaab704a5f331a4e067e65b86a/misc/advent/2023/02/b.py)

## Day 3

A tricky one for an early Sunday! I feel like I made a meal out of it, but AoC feels like that about 75% of the time anyway.

For part one, I got stuck for a while on a program that solved the sample problem but not the full problem. Finally, I [added debugging output](https://github.com/llimllib/personal_code/blob/280691bb0f8d1914f29778525111f3e503414099/misc/advent/2023/03/a.py#L19-L48) and the problem became immediately apparent:

![[Pasted image 20231203141418.png]]

I was counting newline characters as symbols! Everything worked once I stripped the newlines, but I waited way too long to add proper debug output.

**Lesson 1**: quality debugging output is worth its weight in gold
**Lesson 2**: have a low threshold for spending a minute adding debug input

Once I had completed it in a pretty messy way, I thought of a [much neater solution](https://github.com/llimllib/personal_code/blob/master/misc/advent/2023/03/b.py).

For part 2, I made a start at solving it the same way I did part 1: checking each number, then checking if it was connected to a `*`, then checking if was connected to another number.

I almost got it working, but it was super fiddly, when I realized that if I started from the `*` instead of from the numbers, everything would be [much simpler](https://github.com/llimllib/personal_code/blob/master/misc/advent/2023/03/c.py). And it was!

- [messy part 1 with debug output](https://github.com/llimllib/personal_code/blob/master/misc/advent/2023/03/a.py)
- [neat part 1](https://github.com/llimllib/personal_code/blob/master/misc/advent/2023/03/b.py)
- [part 2](https://github.com/llimllib/personal_code/blob/280691bb0f8d1914f29778525111f3e503414099/misc/advent/2023/03/c.py)
- [day 3 problem](https://adventofcode.com/2023/day/3)

## Day 4

Python sets to the rescue.

The [set operators](https://docs.python.org/3/tutorial/datastructures.html#sets) that python added are amazingly helpful when solving AoC problems, and they made short work of today's relatively easy problem. The meat of part 1, after turning the two "hands" into sets, relies on the `&` intersection operator:

```python
def score(a, b):
    intersection = a & b
    return 2 ** (len(intersection) - 1) if intersection else 0


print(sum(score(*parse(line)) for line in sys.stdin))
```

Part 2 I solved as a triply-nested loop; I'm sure there's some easy closed-form solution, but thankfully the problem space was small and we didn't need to find it today:

```python
bonus = defaultdict(int)

for i, line in enumerate(sys.stdin):
    winners, mine = parse(line)
    n = len(winners & mine)
    bonus[i] += 1
    for j in range(bonus[i]):
        for k in range(i + 1, i + n + 1):
            bonus[k] += 1

print(sum(bonus.values()))
```

Later, I noticed that a loop can be removed because we're just adding 1 `bonus[i]` times:

```python
for i, line in enumerate(sys.stdin):
    winners, mine = parse(line)
    n = len(winners & mine)
    bonus[i] += 1
	for k in range(i + 1, i + n + 1):
		bonus[k] += bonus[i]
```

which makes it about 15x faster.

- [part 1](https://github.com/llimllib/personal_code/blob/abb0476459bb5a0d867bab4d36c276608be39a90/misc/advent/2023/04/a.py)
- [part 2](https://github.com/llimllib/personal_code/blob/abb0476459bb5a0d867bab4d36c276608be39a90/misc/advent/2023/04/b.py)
- [problem description](https://adventofcode.com/2023/day/4#part2)

## Day 5

Part 1 was pretty easy; after parsing the file into lists of ranges and adjustments, go through each adjust each seed if it matches a range:

```python
def run(seed: int, intervals: list[list[tuple[tuple[int, int], int]]]) -> int:
    for map in intervals:
        for (a, b), adj in map:
            if a <= seed <= b:
                seed += adj
                break
    return seed


seeds, intervals = parse()
print(min(run(s, intervals) for s in seeds))
```

For part 2, I had an answer that worked in theory but wouldn't finish before the heat death of the universe on the actual puzzle input.

I'm pretty sure that the answer has to do with merging all the ranges into a single list of ranges, but I didn't figure out exactly how to do it.

It's hard for me to write down that I failed on it!

- [part 1](https://github.com/llimllib/personal_code/blob/9b7b9585280940eec1d6ab5acdd083cf71435a0c/misc/advent/2023/05/a.py)
- [problem description](https://adventofcode.com/2023/day/5)

## Day 6

Who needs functions? Today's answer as a pair of one-liners:

```python
in1, in2 = itertools.tee(sys.stdin)

# part 1
print(
    prod(
        sum(1 for p in range(t) if (t - p) * p > d)
        for t, d in zip(*[[int(x) for x in re.findall(r"\d+", line)] for line in in1])
    )
)

# part 2
print(
    prod(
        sum(1 for p in range(t) if (t - p) * p > d)
        for t, d in [[int("".join(re.findall(r"\d+", line))) for line in in2]]
    )
)
```

The only challenge today was converting the problem description into a function:

$$distance = (time limit - press) * press$$

My answer could be a lot more efficient; for one the function is symmetric about the middle so if we started in the middle, we could search outwards in one direction and stop iterating once we found a value that was too low, cutting the search space by roughly 75%.

I also could have actually solved for the intersection of d and the distance function above, but why do more thinking when the computer can just chug? My friend Chris [shows the way](https://github.com/cvermilion/adventofcode/blob/main/2023/06/run.py) if you prefer to think instead of type.

However, the function that stupidly searches the whole space only takes a couple seconds to run on my machine so I just had some fun converting it into single generator expressions.

Also, today I learned about `math.prod`! I'd written my own version so many times but today I decided to check if one existed and [lo and behold, it does](https://docs.python.org/3/library/math.html#math.prod).

- [day 6 answer](https://github.com/llimllib/personal_code/blob/7da47875cf47a193c8e67d4a5431aa5567d163cb/misc/advent/2023/06/a.py)
- [problem description](https://adventofcode.com/2023/day/6)