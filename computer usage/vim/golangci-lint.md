---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
To set the errorfrmat, so I can get the errors in the quickfix (via [this comment](https://github.com/golangci/golangci-lint/issues/895#issuecomment-1103895284)):

`set errorformat=%A%f:%l:%c:\ %m,%-G%.%#`

Then to run it and populate the quickfix (open with `:copen`):

`:cexpr system('golangci-lint run')`

TODO: wrap this up into a nice command