---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
If you have to debug a test that requires you to set the computer time manually, here's how you do it:

```shell
# tell Mac OS not to use the network to get the correct time
$ sudo systemsetup -setusingnetworktime off

# set the date (format is MMDDHHMMYY)
$ sudo date 0519085023
Fri May 19 08:50:00 EDT 2023

# ... now do what you need to do in the given time ...

# when you're done, turn the network time back on
$ sudo systemsetup -setusingnetworktime on
```
