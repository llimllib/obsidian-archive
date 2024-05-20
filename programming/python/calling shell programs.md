---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/amoffat/sh looks like a nice library, similar to what I had started writing for pub so long ago

https://plumbum.readthedocs.io/en/latest/ looks a bit more aggressive, trying to refit pipes into the python bitwise-or operator

(I have never used either of these at all)

My current function I use is some variation of:

```python
def sh(cmd, verbose=False, ignore_errors=False):
    cmd = str(cmd.strip())
    if verbose:
        print(cmd)
    p = subprocess.Popen(cmd, stdout=subprocess.PIPE, shell=True)
    stdout, stderr = [str(x or b"", "utf8") for x in p.communicate()]
    sys.stdout.write(stdout)
    if p.returncode != 0 and not ignore_errors:
        sys.stdout.write(stderr)
        sys.exit(1)
    return [stdout, stderr, p.returncode]
```