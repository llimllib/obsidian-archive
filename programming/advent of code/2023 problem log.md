**WARNING**: spoilers ahead!

- [[2023 problem log#Day 1|day 1]]
- [[2023 problem log#Day 2|day 2]]
- [[2023 problem log#Day 3|day 3]]
- [[2023 problem log#Day 4|day 4]]
- [[2023 problem log#Day 5|day 5]]
- [[2023 problem log#Day 6|day 6]]
- [[2023 problem log#Day 7|day 7]]
- [[2023 problem log#Day 8|day 8]]
- [[2023 problem log#Day 9|day 9]]
- [[2023 problem log#Day 10|day 10]]
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

## Day 7

I got my first couple of guesses wrong today because I have coded poker hand scoring before, and I scored the poker hands like real poker rather than "desert poker".

Instead of ranking them by the order of the cards in the hand (`32222` > `2AAAA` because `3` > `2`), I initially ranked them like you would in real poker, where `2AAAA` beats `32222` because four aces beats four twos.

With the simplified scoring, my answer was boring and straightforward:

```python
def parse(iter):
    hands = []
    faces = {"T": 10, "J": 11, "Q": 12, "K": 13, "A": 14}
    for line in iter:
        hand, bid = line.strip().split(" ")
        hand = [int(faces.get(c, c)) for c in hand]
        hands.append((hand, int(bid)))
    return hands


def score(hand):
    hand, _ = hand
    (_, n), *rest = sorted(
        # turns a hand like [5,6,7,7,7] into [(5, 1), (6, 1), (7, 3)]
        # then, we sort it by count and value so that we have the cards
        # in order of frequency and then rank
        Counter(hand).items(), key=lambda x: (x[1], x[0]), reverse=True
    )

    if n == 5:
        return (7, *hand)
    (_, nn) = rest.pop(0)
    if n == 4:
        return (6, *hand)
    if n == 3 and nn == 2:
        return (5, *hand)
    if n == 3:
        return (4, *hand)
    if n == 2 and nn == 2:
        return (3, *hand)
    if n == 2:
        return (2, *hand)
    return (1, *hand)
```

I have only ever used [collections.Counter](https://docs.python.org/3/library/collections.html#collections.Counter) for advent of code, but boy is it handy for AoC.

With a scoring function written, all that's left is to parse the hands and sum the winnings:

```python
hands = parse(sys.stdin)
print(sum((i + 1) * bid for i, (_, bid) in enumerate(sorted(hands, key=score))))
```

To solve part 2, I changed the value of a jack from 11 to 1, and only had to make minor alterations to the score function:

```python
def score(hand):
    hand, _ = hand
    js = hand.count(1)
    (top, n), *rest = sorted(
        Counter(hand).items(), key=lambda x: (x[1], x[0]), reverse=True
    )
    if top == 1:
        n = rest.pop(0)[1] if rest else 0

    if n + js == 5:
        return (7, *hand)
    nn = rest.pop(0)[1] if rest else 0
    if n + js == 4:
        return (6, *hand)
    if n + nn + js == 5:
        return (5, *hand)
    if n + js == 3:
        return (4, *hand)
    if n + nn + js == 4:
        return (3, *hand)
    if n + js == 2:
        return (2, *hand)
    return (1, *hand)
```

Thanks to my friend Chris who pointed out that all we care about for ranking hands is the cardinality of ranks (i.e. the number of each rank in the hand), leading to this terrible golfed generator expression for part 1 that eliminates the `score` and `parse` functions entirely:

```python
print(
    sum(
        (i + 1) * bid
        for i, (_, bid) in enumerate(
            sorted(
                [
                    (
                        [
                            int({"T": 10, "J": 11, "Q": 12, "K": 13, "A": 14}.get(c, c))
                            for c in cards
                        ],
                        int(bid),
                    )
                    for cards, bid in [line.split(" ") for line in sys.stdin]
                ],
                key=lambda hb: list(sorted(Counter(hb[0]).values(), reverse=True))
                + hb[0],
            )
        )
    )
)
```

- [part 1](https://github.com/llimllib/personal_code/blob/29fced1e0938b73b27d1ab9b75b23545eda08f0b/misc/advent/2023/07/a.py)
- [part 2](https://github.com/llimllib/personal_code/blob/29fced1e0938b73b27d1ab9b75b23545eda08f0b/misc/advent/2023/07/b.py)
- [problem description](https://adventofcode.com/2023/day/7)

## Day 8

A day where a tiny bit of thinking saves you from wasting your computer's processing power. If you try to run part 2 until it finishes, you're likely to be waiting a long while.

First, parse the network into a dictionary:

```python
def parse(iter):
    directions = [1 if c == "R" else 0 for c in list(next(iter).strip())]
    next(iter)
    network = {}
    for line in iter:
        a, l, r = re.findall(r"\w+", line)
        network[a] = (l, r)
    return (directions, network)
```

Next, you need a function for finding the length of a cycle (from an `A` node to a `Z` node):

```python
def cycle_len(directions, network, loc):
    for i, dir in enumerate(itertools.cycle(directions)):
        loc = network[loc][dir]
        if loc[-1] == "Z":
            return i + 1
```

for part 1, find the cycle length for `AAA`:

```python
directions, network = parse(sys.stdin)
print(cycle_len(directions, network, "AAA"))
```

for part 2, find the least common multiple (using [numpy.lcm](https://numpy.org/doc/stable/reference/generated/numpy.lcm.html)) of the cycle length of all nodes ending with `A`:

```python
print(
    np.lcm.reduce(
        [cycle_len(directions, network, node) for node in network if node[-1] == "A"]
    )
)
```

_update:_ Today I learned that there is a [math.lcm](https://docs.python.org/3/library/math.html#math.lcm) in the standard library, since version 3.9! I love removing dependencies.

```python
print(
    math.lcm(
        *(cycle_len(directions, network, node) for node in network if node[-1] == "A")
    )
)
```

- [day 8 solution](https://github.com/llimllib/personal_code/blob/29292348e730fbef87860cb43db12dda972f2bd1/misc/advent/2023/08/a.py)
- [problem description](https://adventofcode.com/2023/day/8)

## Day 9

I thought this one was going to require me to figure out the math, but a simple iterative model was plenty fast enough.

For part 1, we want to find the sum of the numbers added to the sequence. First I take the differences and save the final number of each list:

```python
ls = []
while any(a != b for a, b in itertools.pairwise(ints)):
    ls.append(ints[-1])
    ints = [b - a for a, b in itertools.pairwise(ints)]
```

Then I build back up the sum and return it:

```python
sum = ints[0]
for b in reversed(ls):
	sum += b
return sum
```

At this point, I noticed that "sum" is equal to the additional number (`ints[0]`) and the last number of each row, simplifying that to:

```python
return sum([ints[0]] + ls)
```

For part 2, the first half of the answer is the same, except I save the first number in each row instead of the last. Then build back up to the first value by taking the difference of the first number and the current value:

```python
    cur = ints[0]
    for b in reversed(ls):
        cur = b - cur
    return cur
```

I'm sure there's a similar simplification of this process, but I'm feeling a little dense this morning and I'm leaving it where it is.

To parse the input and print the results, I have:

```python
in1, in2 = itertools.tee(sys.stdin)
print(sum(part1([int(x) for x in line.split()]) for line in in1))
print(sum(part2([int(x) for x in line.split()]) for line in in2))
```

_update_: I realized that part 2 is the reverse of part 1! So you can remove the `part2` function and express part 2 in terms of part 1 as:

```python
in1, in2 = itertools.tee(sys.stdin)
print(sum(part1([int(x) for x in line.split()]) for line in in1))
print(sum(part1(list(reversed([int(x) for x in line.split()]))) for line in in2))
```

- [day 9 solution](https://github.com/llimllib/personal_code/blob/f0c09f2be4c856c04bcf85ed195375fa60b8722f/misc/advent/2023/09/a.py)
- [problem description](https://adventofcode.com/2023/day/9#part2)

## Day 10

Phew, that was a lot!

I got part 1 reasonably easily, but had to cheat for part 2 by looking at the answers thread.

I had a vague sense for part 2 that there was a parity-based solution, but I had to look at somebody else's answer for how to implement it.

I'm just going to post the link to my code, it's a bit of a mess and I don't feel like writing about it today.

- [day 10 solution](https://github.com/llimllib/personal_code/blob/2efbb42e2f116cc2eea685181fcd51c486f6e15f/misc/advent/2023/10/a.py)
- [problem description](https://adventofcode.com/2023/day/10)