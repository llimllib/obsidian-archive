---
created: 2025-12-03T00:43:06.843Z
updated: 2025-12-03T00:43:06.843Z
---
This year I've decided to do Advent of Code in [[Gleam]], a programming language I know nothing about and have never written a line of code in.

Previously: [[Advent of Code 2024]], [[2023 problem log]], and incomplete answers back to 2015 [in github](https://github.com/llimllib/personal_code/tree/master/misc/advent/)

- [[Advent of Code 2025#day1|day 1]]
- [[Advent of Code 2025#day2|day 2]]

## Day 1

Not the easiest day 1! The problem centered around a [ring](https://en.wikipedia.org/wiki/Ring_(mathematics)) of the numbers 0-99. 

- My answer for both parts is [here](https://github.com/llimllib/personal_code/blob/master/misc/advent/2025/advent/src/day01/a.gleam)
- I struggled with coming up with a simple way to express the crossings of zero for the second part, and I'm not super happy with how that came out
- You need a library to read files in gleam! `gleam add simplifile` to get the standard sync library it seems
- `echo` is super handy for debugging pipelines - just stick it between `|>` braces and it will show you what's going on
- I ought to figure out a better way to handle errors than just `unwrap`ing them and picking a random default value, it's definitely going to bite me eventually if I don't panic. I'm surprised there's not an `unwrap_or_panic` or something like that! Maybe I'll write it as `must` or something, but for today I just got by

## Day 2

It seems that the creator of gleam doesn't like tuples, so today I tried not to use any. I started with a custom type to represent a range:

```gleam
pub type Range {
  Range(start: Int, end: Int)
}
```

For part 1, I used a generative approach where I iterated from the start of each range through the end, and checked if the number was of the form `<x><x>`. The heart of it is this function:

```gleam
pub fn acc_dubs(front: Int, range: Range, acc: List(Int)) {
  let dub =
    string.append(int.to_string(front), int.to_string(front))
    |> int.parse
    |> result.unwrap(0)
  case dub >= range.start, dub <= range.end {
    True, True -> acc_dubs(front + 1, range, [dub, ..acc])
    True, False -> acc
    False, True -> acc_dubs(front + 1, range, acc)
    False, False -> panic as "impossible"
  }
}
```

For part 2, I got in loops thinking about how to generate all possible combinations of numbers, so I instead took a filtering approach. This function checks if a number is symmetric in the way the problem states (assuming that there are no numbers with more than 10 digits):

```gleam
pub fn is_sym(n) {
  let ns = n |> int.to_string
  let l = ns |> string.length
  list.any(
    [
      atoi(string.repeat(string.slice(ns, 0, 1), int.max(l, 2))),
      atoi(string.repeat(string.slice(ns, 0, 2), int.max(l / 2, 2))),
      atoi(string.repeat(string.slice(ns, 0, 3), int.max(l / 3, 2))),
      atoi(string.repeat(string.slice(ns, 0, 4), int.max(l / 4, 2))),
      atoi(string.repeat(string.slice(ns, 0, 5), int.max(l / 5, 2))),
    ],
    fn(x) { x == n && n > 9 },
  )
}
```

I find that pleasing!

Then I iterated over every number in each range and checked it for symmetry, and summed the result:

```gleam
pub fn part_b(input) {
  let ranges = parse(input)
  list.fold(
    list.flat_map(ranges, fn(r) { acc_nubs(r.start, r.end, []) }),
    0,
    int.add,
  )
}

pub fn acc_nubs(start, end, acc) {
  case start > end, is_sym(start) {
    True, _ -> acc
    _, True -> acc_nubs(start + 1, end, [start, ..acc])
    _, False -> acc_nubs(start + 1, end, acc)
  }
}
```