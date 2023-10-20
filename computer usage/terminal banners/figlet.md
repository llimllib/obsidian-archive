http://www.figlet.org has been the answer for a long time.

Here's a little script to print your message in a few of the default fonts:

```bash
message='lilium'
fonts=(slant shadow small big script digital bubble banner lean)
for f in "${fonts[@]}"; do
    printf -- "-------- %s\n\n" "$f"
    figlet -f "$message"
done
```

you can go [here](http://www.figlet.org/examples.html) to see lots more examples of fonts you can get.

[pyfiglet](https://github.com/pwaller/pyfiglet) is handy also, and what I used in [limbo](https://github.com/llimllib/limbo/blob/master/limbo/plugins/banner.py)