I have a two-line prompt, and I wanted the right prompt to line up with the first line of the left prompt, not the second; this makes copying and pasting commands much easier. To do so was a bit tricky and required some googling:

```shell
# The right prompt should be on the same line as the first line of the left
# prompt. To do so, there is just a quite ugly workaround: Before zsh draws
# the RPROMPT, we advise it, to go one line up. At the end of RPROMPT, we
# advise it to go one line down. See:
# http://superuser.com/questions/357107/zsh-right-justify-in-ps1
local RPROMPT_PREFIX='%{'$'\e[1A''%}' # one line up
local RPROMPT_SUFFIX='%{'$'\e[1B''%}' # one line down

# show the current time on the right
export RPROMPT="${RPROMPT_PREFIX}%F{magenta}%F{black}%K{magenta}%t${RPROMPT_SUFFIX}"
```
![[Pasted image 20230710213053.png]]

[source in context here](https://github.com/llimllib/personal_code/blob/cca8ce2a68d0bc53455d555d7b9a7a9f79a55ee8/homedir/.zshrc#L108-L120)