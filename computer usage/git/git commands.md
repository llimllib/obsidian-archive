### Show the history of a particular file:

`git log -p -- .github/workflows/deploy-staging.yml`

### search the commit log

`git log --grep migrations`

### print each local branch name and its corresponding remote

`git branch --format "%(refname:short) %(upstream)"`

(useful for seeing what branches you have locally that haven't been pushed)