---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Take 2 from https://replicate.com/blog/run-stable-diffusion-on-m1-mac:

```
$ git clone -b apple-silicon-mps-support https://github.com/bfirsh/stable-diffusion.git
Cloning into 'stable-diffusion'...
remote: Enumerating objects: 394, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 394 (delta 7), reused 12 (delta 7), pack-reused 378
Receiving objects: 100% (394/394), 42.66 MiB | 11.73 MiB/s, done.
Resolving deltas: 100% (156/156), done.

$ cd stable-diffusion
$ mkdir -p models/ldm/stable-diffusion-v1/
$ python -mvenv stable-diffusion-enva
$ source stable-diffusion-env/bin/activate
$ pip install -r requirements.txt
```

- go to https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/blob/main/sd-v1-4.ckpt and download the file (since I've already logged in and accepted the terms for the file)
- this is what we previously did with git-lfs
  - but now that repo has another large checkpoint file, so let's just get this file manually
  - for kicks, I grabbed the CDN URL and am downloading it with https://github.com/melbahja/got

```
$ got -o models/ldm/stable-diffusion-v1/model.ckpt \
  https://cdn-lfs.huggingface.co/repos/4c/37/4c372b4ebb57bbd02e68413d4951aa326d4b3cfb6e62db989e529c6d4b26fb21/fe4efff1e174c627256e44ec2991ba279b3816e364b49f9be2abc0b3ff3f8556

# Now it works! 
# Make sure you have the virtualenv you created earlier active
(stable-diffusion-env) $ python scripts/txt2img.py   --prompt "astronaut eating an apple in space, digital photograph"   --n_samples 1 --n_iter 1 --plms
```

To remove the safety filter: replace line 324 of scripts/txt2img.py:

```python
x_checked_image, has_nsfw_concept = check_safety(x_samples_ddim)
```

with:

```python
x_checked_image = x_samples_ddim
```

----------
news.yc [suggests](https://news.ycombinator.com/item?id=32680293) to try the [lstein fork](https://github.com/lstein/stable-diffusion/blob/main/README-Mac-MPS.md) for better performance?

ok, sure.

```
$ brew install protobuf # I already had cmake and rust
$ git clone https://github.com/lstein/stable-diffusion lstein-stable-diffusion
$ cd lstein-stable-diffusion
$ ln -sf ~/code/tmp/stable-diffusion/stable-diffusion/models/ldm/stable-diffusion-v1 models/ldm/stable-diffusion-v1
$ python -mvenv sdenv
$ source sdenv/bin/activate
# ugh conda
$ CONDA_SUBDIR=osx-arm64 conda env create -f environment-mac.yaml
$ conda activate ldm
$ python scripts/preload_models.py
$ python scripts/dream.py --full_precision
```


------

Previous attempt that kind-of-worked:

working from:

https://zenn.dev/bellbind/scraps/ea15aab699dde9

```
$ brew install git-lfs
$ git lfs install --skip-smudge
$ brew install anaconda
$ /opt/homebrew/anaconda3/bin/conda install bash
$ exit
```

On trying to do the "lfs install" step, I got:

```
$ git lfs install --skip-smudge
warning: the "filter.lfs.clean" attribute should be "git-lfs clean -- %f" but is "git-lfs c
lean %f"
Run `git lfs install --force` to reset Git configuration.
```

maybe from old configuration? I seemed to solve it with:

```
$ git lfs install --force
Git LFS initialized.
$ git lfs install --skip-smudge
Git LFS initialized.
```

I think that first "conda install bash" was supposed to be "conda init bash" instead

```
# this requires your huggingface username and password, and you have to go to
# https://huggingface.co/CompVis/stable-diffusion-v-1-4-original and accept the
# license
$ git clone  https://huggingface.co/CompVis/stable-diffusion-v-1-4-original
$ cd stable-diffusion-v-1-4-original

# this takes a while, it downloads a 4gb file
$ git lfs pull
$ cd ..

$ git clone https://github.com/magnusviri/stable-diffusion.git
$ cd stable-diffusion
$ git switch apple-silicon-mps-support

# here the author asks you to update some versions but it wasn't clear to me
what I was supposed to do, so I'm trying out doing... nothing
$ vim environment-mac.yaml
```

`conda init bash` makes conda change my PS1 on every startup by default! This is very annoying (and bad form from conda I think) and I will have to figure out how to fix that.

(update: `conda config --set auto_activate_base false` does the job)

```
$ conda env create -f environment-mac.yaml
$ conda activate ldm
$ conda install -y pytorch torchvision torchaudio -c pytorch-nightly
$ mkdir models/ldm/stable-diffusion-v1
$ mv ../stable-diffusion-v-1-4-original/sd-v1-4.ckpt models/ldm/stable-diffusion-v1/model.ckpt
```

Then the author suggests changing a line of code in the torch package... but that line of code doesn't exist. Hrmph.

Well, let's see how it goes giving it a shot anyway.

Hey, it worked!

```
python scripts/txt2img.py --prompt "Aperson playing soccer in the style of Edward Gorey" --plms --n_samples 1 --n_iter 1
```

didn't produce a very _good_ image but it did produce one

Next up, I tried `A painting of the Portland Head Light Lighthouse in the style of Monet`, but got hit by the safety filter! [This post](https://www.reddit.com/r/StableDiffusion/comments/wv2nw0/tutorial_how_to_remove_the_safety_filter_in_5/) showed how to disable it.

Finally, I tried `A stained glass window depicting a falcon carrying a fish in its talons` and got barely recognizable images out of it.

I'm getting utter crap out of it, unfortunately, nothing like what I see on the web, and I don't have the motivation to figure out why so I'm probably just going to delete it.

I'm sure it won't be long before there is better stuff more easily available.
