---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/geohot/tinygrad

Library from George Hotz focused on creating the smallest possible useful deep learning library.

Check the examples dir, for ex the [mnist](https://github.com/geohot/tinygrad/blob/c48fc47d01696ce9f82db7184794ad0b74e8a78f/examples/mnist_gan.py) example that only uses 145 lines

```
# from the root dir of the repo
python examples/mnist_gan.py
```

on my computer each epoch takes about 3 minutes, so training the whole net (300 epochs) would take about 15 hours.

I saw in the source that there is a metal interface, but no idea if it's being used.