https://jacobtomlinson.dev/effver/

![[Pasted image 20240216085956.png]]

> EffVer follows the same pattern of incrementing numbers to communicate with users that SemVer does, and is forward and backward compatible with SemVer (you don’t need to use something like a [Python version epoch](https://packaging.python.org/en/latest/specifications/version-specifiers/#version-epochs) to switch between the two schemes). The difference is that instead of quantifying the orthogonality of a change EffVer tries to quantify the intended work required to adopt the change.

In a world where somebody relies on every observable behavior of your program, there's no sense in trying to guess if you've broken backwards compatibility or not.

I think this scheme captures the reality of semantic versioning pretty well, and doesn't promise what it can't deliver. Fun idea.