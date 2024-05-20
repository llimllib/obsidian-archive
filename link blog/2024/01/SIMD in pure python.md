---
updated: '2024-01-05T15:30:22Z'
created: '2024-01-05T15:30:22Z'
---
https://www.da.vidbuchanan.co.uk/blog/python-swar.html

Fun blog post where the author goes through what SIMD is, and demonstrates how you can get python to use it under the hood (on their computer at least), then writes a very fast Life simulation using the knowledge.

Basically, they show the code that interprets this function:

```python
def xor_bytes_simd(a: bytes, b: bytes) -> bytes:
    assert(len(a) == len(b))
        return (
            int.from_bytes(a, "little") ^ int.from_bytes(b, "little")
        ).to_bytes(len(a), "little")
```

compiles down to NEON assembly (the ARM equivalent of SIMD) on their Apple Silicon computer, by decompiling python.

> The key observation here is that our "pseudo-SIMD" implementation is using real SIMD instructions under the hood! At least, it is on my system; this may depend on your platform, compiler, configuration, etc.

_then_ after all that, they build the game of life strictly out of operations on integers, with a code snippet that I don't understand but I would like to take a minute at some point to go through:

```python
# count neighbors
summed = state
summed += (summed >> 4) + (summed << 4)
summed += (summed >> COLSHIFT) + (summed << COLSHIFT)

# check if there are exactly 3 neighbors
has_3_neighbors = summed ^ MASK_NOT_3 # at this point, a value of all 1s means it was initially 3
has_3_neighbors &= has_3_neighbors >> 2 # fold in half
has_3_neighbors &= has_3_neighbors >> 1 # fold in half again

# check if there are exactly 4 neighbors
has_4_neighbors = summed ^ MASK_NOT_4 # at this point, a value of all 1s means it was initially 4
has_4_neighbors &= has_4_neighbors >> 2  # fold in half
has_4_neighbors &= has_4_neighbors >> 1  # fold in half again

if cfg.drylife:
    # check if there are exactly 7 neighbors
    has_7_neighbors = summed ^ MASK_NOT_7 # at this point, a value of all 1s means it was initially 7
    has_7_neighbors &= has_7_neighbors >> 2  # fold in half
    has_7_neighbors &= has_7_neighbors >> 1  # fold in half again

    # variable name here is misleading...
    has_3_neighbors |= (~state) & has_7_neighbors

# apply game-of-life rules
state = (has_3_neighbors | (state & has_4_neighbors)) & MASK_CANVAS
```

[full source here](https://github.com/DavidBuchanan314/pyswargol/blob/bb8a748065bbe6f7a1c0bf4a331b42e178e9d821/swargol.py)