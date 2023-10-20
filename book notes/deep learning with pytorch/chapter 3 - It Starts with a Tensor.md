- "floating point numbers are the way a network deals with information"
	- "In the context of deep learning, tensors refer to the generalization of vectors and matrices to an arbitrary number of dimensions,"
	- unlike numpy arrays, torch tensors have the ability to run on GPUs, distribute operations to multiple computers, and track the graph of computations that created them
- [notes on using tensors in this ipython notebook](https://github.com/llimllib/torchbook/blob/main/chap3/basic%20tensor%20operations.ipynb)
	- squeezing and unsqueezing
	- broadcasting
	- named tensors
		- which will not be used in the book, due to their experimental nature
- Tensor element types
	- the [tensor documentation](https://pytorch.org/docs/stable/tensors.html#data-types) lists the availble types
	- `float32` default
		- `float16` can be useful, as it is a default data type on modern GPUs and often the extra precision of 32 bits does not buy you useful training results
	- tensors used as indexes into other tensors are expected to be `int64`
	- predicates on tensors produce `bool` result tensors
	- [notebook with examples](https://github.com/llimllib/torchbook/blob/main/chap3/tensor%20types.ipynb)

## Types of operations

- The types of operations
	- The torch docs are thorough, but here's an overview:
	- [Creation operations](https://pytorch.org/docs/stable/torch.html#creation-ops)
		- `ones`, `zeros`, `rand`, `from_numpy`, `range`, `linspace`, `full` (fill with a given value)
	- [Pointwise operations](https://pytorch.org/docs/stable/torch.html#pointwise-ops)
		- return a new tensor by applying a function to each element independently
		- `abs`, `cos`, `add`, bitwise ops, `pow`
	- [Reduction operations](https://pytorch.org/docs/stable/torch.html#reduction-ops)
		- aggregate values by iterating through tensors
		- `mean`, `std`, `norm`, `all`, `quantile`
	- [Comparison operations](https://pytorch.org/docs/stable/torch.html#comparison-ops)
		- functions for evaluating numerical predicates over tensors
		- `equal`, `max`
	- [Spectral operations](https://pytorch.org/docs/stable/torch.html#spectral-ops)
		- functions for transofrming in and operating in the frequency domain
		- All the stuff from DSP I don't understand!
		- `hamming_window`, `stft` (short-time fourier transform)
	- [Other operations](https://pytorch.org/docs/stable/torch.html#other-operations)
		- `clone`, `cross`, `flatten`, `histogram`,  `renorm`, `trace` (sum of elements of diagonal)
	- [BLAS and LAPACK operations](https://pytorch.org/docs/stable/torch.html#blas-and-lapack-operations)
		- fast matrix math

## Storage

- values in tensors are allocaetd in contiguous chunks of memory managed by `torch.Storage`
- storage is 1d, and a tensor is a view of storage capable of idnexing into it with an offset and strides
	- as such, multiple tensors can index the same storage
- [notebook with more info and some storage examples](https://github.com/llimllib/torchbook/blob/main/chap3/tensor%20storage.ipynb)
- tensors are defined by three metadata
	- **size** is a tuple indicating how many elements across each dimension the tensor represents
	- **offset** is the index in the storage corresponding to the first element in the tensor
	- **stride** is the number of elements in the storage that need to be skipped over to obtain the next element along each dimension
- in a 2d tensor, accessing element `(i,j)` is:`offset + (stride[0]*i) + (stride[1]*j)`
- operations that don't reallocate `storage` are cheap
	- transposition or extracting a subtensor, for example
- You can use `clone()` to allocate a tensor with new storage
- There is a shorthand for `transpose` - `t`
	- but it doesn't work with specifying dimensions - [it expects a 2d tensor](https://pytorch.org/docs/stable/generated/torch.t.html?highlight=torch+t#torch.t)
- You can transpose in multiple dimensions by specifying which dimensions should be transposed
- A tensor whose values are laid out in storage from the rightmost dimension onwards is called `contiguous`
	- What is the "rightmost dimension"? I don't understand this at all
	- contiguous tensors have improved efficiency because we can iterate them efficiently
		- improved cache locality
	- Some functions only work on contiguous tensors
	- `is_contiguous` will tell us if our tensor is or is not
	- a transpose of a contiguous tensor will not be contiguous
	- we can use the `contiguous` method to obtain a contiguous tensor from a non-contiguous one
		- It will reallocate
	- The final example in the section helps me understand a bit better what contiguous means, so I'll copy it in here from the notebook referenced above

```python
In [23]: p = torch.tensor([[4,1],[5,3],[2,1.0]])
    ...: p_t = p.t()
    ...: p_t, p_t.storage(), p_t.stride(), p_t.is_contiguous()

Out[23]: (tensor([[4., 5., 2.],
         [1., 3., 1.]]),
          4.0
          1.0
          5.0
          3.0
          2.0
          1.0
         [torch.storage.TypedStorage(dtype=torch.float32, device=cpu) of size 6],
         (1, 2),
         False)


In [24]: p_t_c = p_t.contiguous()
    ...: p_t_c, p_t_c.storage(), p_t_c.stride()

Out[24]: (tensor([[4., 5., 2.],
         [1., 3., 1.]]),
          4.0
          5.0
          2.0
          1.0
          3.0
          1.0
         [torch.storage.TypedStorage(dtype=torch.float32, device=cpu) of size 6],
         (3, 1))
 ```

## Moving tensors to the GPU

- You can specify the `device` as a keyword argument to the tensor
- devices
	- `cuda` is the device for nvidia GPUs
	- `MPS` is the device for M1 macs (Metal Pixel Shader)
		- [this issue](https://github.com/pytorch/pytorch/issues/77764) tracks coverage for torch operaions on the MPS device
		- the gaps are still significant
	- `cpu` is the device for the CPU
- To copy a CPU tensor to the GPU, use `to` with the `device` kwarg
- [check out the notebook](https://github.com/llimllib/torchbook/blob/main/chap3/moving%20tensors%20to%20the%20GPU.ipynb)

## Numpy compatibility

- call `numpy()` on a tensor to get a numpy array out
	- will share storage with the tensor
- call `torch.from_numpy(array)` to get a tensor out
	- will also share storage
	- note that numpy defaults to float64, while float32 or float16 are best for us, so you might want to change the dtype

## serializing tensors

- calling `torch.save(tensor, filename)` will save the tensor to a pickle at `filename`
	- can also pass a file handle as the second arg
- `torch.load(filename | file_handle)` will return the tensor
- Both of those methods save it in a pickle format, which is not great for interop
- we can use `h5py` to save tensors as HDF5
	- http://www.h5py.org
- book doesn't mention parquet, but torch seems to have libraries for it

## exercises

[notebook](https://github.com/llimllib/torchbook/blob/main/chap3/exercises.ipynb)