https://rsync.samba.org

The classic file syncing program

----

for a useful progress display without echoing every file to the terminal, try `--info=progress2`:

for example: `rsync -a --info=progress2 ../branch/node_modules ./node_modules` won't print every file it copies in the node_modules dir, which is enormous, but will print useful progress.