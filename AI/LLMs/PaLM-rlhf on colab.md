Messing around with [this repository](https://github.com/lucidrains/PaLM-rlhf-pytorch)

1. Start a new colab notebook
2. switch the runtime to GPU by going to *Runtime* -> *Change Runtime Type*
	1. You can create a cell with `!nvidia-smi` if you want to check that you have a GPU; it will fail if you don't
3. `!pip install palm_rlhf_pytorch`

I set up a Colab based on [this file](https://github.com/lucidrains/PaLM-rlhf-pytorch/blob/f68733927414d1eb72f9ed79c578fbbc3624e179/train.py) but I couldn't train it because it took too long