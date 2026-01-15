---
created: 2025-11-17T21:45:35.644Z
updated: 2025-11-17T21:45:35.644Z
---
`eslogger` is a super useful debugging tool for Mac OS X, which sadly does not appear to even merit a single webpage at apple.com.

example: monitor files `stat`ed by a process named `git`, and print out just their path
```
sudo eslogger stat |
    jq -r 'select(.process.executable.path | test("/git$")) | .event.stat.target.path'
```
		
- list event types with `eslogger --list-events`
- monitor the events you're interested in with `sudo eslogger [event types...]`
- For example, `eslogger stat write unlink create` will show you file events in a jsonl format
- the `jsonl` format also means you can use `jq` to process the events. Here's a command that will list just the executables that get `exec`ed on your system:
	- `sudo eslogger exec | jq -r '.event.exec.target.executable.path'`

cf [[debugging os x]]