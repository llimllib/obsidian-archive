**WARNING**: spoilers ahead!
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