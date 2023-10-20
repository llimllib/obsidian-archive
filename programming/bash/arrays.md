To read the output of a command (naively) into an array:

```bash
$ grep iresome /usr/share/dict/words
tiresome
tiresomely
tiresomeness
tiresomeweed
# store the above list as an array
$ iresome=( $(grep iresome /usr/share/dict/words) )
# use declare -p to peek at the values in an array
$ declare -p iresome
declare -a iresome=([0]="tiresome" [1]="tiresomely" [2]="tiresomeness" [3]="tiresomeweed")
```

Simple! but doesn't work if they have spaces due to bash's always-infernal IFS

```bash
$ curl -s https://www.google.com | prettier --parser html | grep 'span>'
          ><span id="gbn" class="gbi"></span><span id="gbf" class="gbf"></span
                    type="submit" /></span></span
              ></span>
            /><span>Calling all young artists: Submit your artwork for </span
$ spans=( $(curl -s https://www.google.com | prettier --parser html | grep 'span>') )
$ declare -p spans
declare -a spans=([0]="><span" [1]="id=\"gbn\"" [2]="class=\"gbi\"></span><span" [3]="id=\"gbf\"" [4]="class=\"gbf\"></span" [5]="type=\"submit\"" [6]="/></span></span" [7]="></span>" [8]="/><span>Calling" [9]="all" [10]="young" [11]="artists:" [12]="Submit" [13]="your" [14]="artwork" [15]="for" [16]="</span")
```

We _could_ fix this by changing IFS to just a newline, but then bash will still fail if the command substitution contains wildcards that match filenames.

Bash _desperately_ wants to match file names, which is usually useful! but sometimes annoying.

The `readarray` builtin is the proper way to do this:

```bash
$ readarray -t spans < <(curl -s https://www.google.com | prettier --parser html | grep 'span>')
$ declare -p spans
declare -a spans=([0]="          ><span id=\"gbn\" class=\"gbi\"></span><span id=\"gbf\" class=\"gbf\"></span" [1]="                    type=\"submit\" /></span></span" [2]="              ></span>" [3]="            /><span>Calling all young artists: Submit your artwork for </span")
```

`readarray` is only available on bash >4, google up how to use `read` to do this on older bashes if you need that-t