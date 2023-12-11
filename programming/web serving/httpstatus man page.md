https://github.com/jschauma/httpstatus

is a great idea, a simple little man page that lists every HTTP status and a short description.

To install it on an arm mac, if you're a homebrew user you can do:

`curl 'https://raw.githubusercontent.com/jschauma/httpstatus/main/httpstatus.7' -o $(brew --prefix)/share/man/man7/httpstatus.7`

Change the path to your manual as appropriate for other systems.

Then, `man httpstatus` will bring it up.