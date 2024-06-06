---
created: 2024-06-06T16:41:32.369Z
updated: 2024-06-06T16:41:32.369Z
---
If you've published a package to github's [npm registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry), the documentation tells you to create a Personal Access Token. This is an unfortunately un-scriptable process.

Thankfully, it is possible to use the `gh` command line tool to create a usable token. Since it's poorly documented, I've written this note; it assumes you have [gh installed](https://github.com/cli/cli?tab=readme-ov-file#installation) already.

1. `gh auth login --scopes=write:packages`
	1. This will guide you through a process to create a token with `write:packages` scope, which allows you to read and write npm packages to the github repository
2. `npm config set -g //npm.pkg.github.com/:_authToken $(gh auth token)`
	1. This globally configures npm to use the token you just generated when authenticating to `npm.pkg.github.com`
3. `npm config set -g @your_scope:registry https://npm.pkg.github.com/` 
	1. This command globally configures npm to use the github package registry for the scope containing your package
	2. My advice is to use a particular [scope](https://docs.npmjs.com/cli/v9/using-npm/scope) for the packages you want to live on the github package repository; it is not easily possible to have npm switch between registries if you have some packages on regular npm and others on the github package repository

To test that you have access, you can do `npm install -g @your_scope/some_package` and verify that you are able to install your private package.