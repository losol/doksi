---
name: Deploy with Github actions
route: /deploy/github_actions
menu: Deployment
---

# Deploy documentation automatic with Github Actions

## Add workflow to source code

Create a new file in your source repository, named `.github/workflows/deploy_docs.yml`

It could contain an action with this steps:

```yaml
name: Deploy documentation

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v1

      - name: Set Node.js
        uses: actions/setup-node@v1
        with:
          node-version: 10.x

      - name: Install npm dependencies
        working-directory: ./docs
        run: npm install

      - name: Run tests
        working-directory: ./docs
        continue-on-error: false
        run: npm run test

      - name: Deploy pages
        working-directory: ./docs
        run: |
          git config --global user.name "Spark documentation bot"
          git config --global user.email "spark@docbot.com"
          npx gatsby build --prefix-paths && npx gh-pages -d public -r https://${{ secrets.GH_TOKEN }}@github.com/losol/doksi.git
```

Please remember to change the link to your own git repository.

## Get personal access token

In GitHub Settings -> Developer -> Personal access token, create a new Personal access token with repo scope:
![image](https://user-images.githubusercontent.com/17168367/69485965-ad869780-0e46-11ea-91a3-dbbdf6c70be3.png)

## Add repo secret

Then add a new secret to the repo settings, with name `GH_TOKEN`

![image](https://user-images.githubusercontent.com/17168367/69485949-4b2d9700-0e46-11ea-92f7-8b3098913918.png)
