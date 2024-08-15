---
updated: 2024-08-15T14:05:25.876Z
created: 2024-02-28T15:41:50Z
---
To publish an observable framework website on github pages is a 2-step procedure:

1. Go to settings -> pages (The URL will be `https://github.com/<user>/<repo>/settings/pages`) and change the "source" dropdown from "deploy from a branch"  to "Github Actions"
2. Add the file below to the repository as `.github/workflows/publish.yml`
3. That's it! Every time you push a change to the main branch you'll get an updated website.

```yaml
name: Publish
on:
  workflow_dispatch:
  push:
    branches: ["main"]
permissions:
  contents: write
jobs:
  build:
    concurrency: ci-${{ github.ref }} # Recommended if you intend to make multiple deployments in quick succession.
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: "npm"

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

If you would like the site to update regularly, add a `cron` trigger to the `on` block. Here's an example `on` block that would rebuild it daily, and also on changes to `main` or by manually triggering it:

```yaml
on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * *'
  push:
    branches: ["main"]
```