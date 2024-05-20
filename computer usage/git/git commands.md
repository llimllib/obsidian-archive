---
updated: '2024-04-26T19:29:14Z'
created: '2023-10-20T13:54:09Z'
---
### Show the history of a particular file:

`git log -p -- .github/workflows/deploy-staging.yml`

### search the commit log

`git log --grep migrations`

### print each local branch name and its corresponding remote

`git branch --format "%(refname:short) %(upstream)"`

(useful for seeing what branches you have locally that haven't been pushed)

## show the history of a branch since it diverged from the main branch

`git diff $(git merge-base --fork-point main)`

If you want to use a branch other than the current branch, you need to specify it twice:

`git diff $(git merge-base --fork-point main some-branch)..some-branch`