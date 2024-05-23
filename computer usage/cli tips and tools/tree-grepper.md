---
created: 2024-05-23T12:09:22.986Z
updated: 2024-05-23T12:09:22.986Z
---
https://github.com/BrianHicks/tree-grepper

uses [[tree-sitter]] to parse source code into ASTs and allow you to grep it via queries.

explanatory blog post: https://bytes.zone/posts/tree-grepper/

The example given in that post is, "build an import graph for my source code", a task I've [previously accomplished](https://github.com/llimllib/personal_code/blob/master/bash/monorepo_dependencies/deps.graphviz.bash#L14-L21) with jq or terrible regexes. In that particular case, I relied on `package.json` exactly because it's easily parseable; but perhaps it would have been better to rely on a tool that parsed the source instead.

Unfortunately, the tool doesn't have any releases yet and requires nix to build, so I'm not willing to go quite that far, so I can't play with it.

See also [[ast-grep]]
