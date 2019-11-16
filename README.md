# Doczy

A starter for adding documentation as code to a project. This documentation template is built on Gatsby v2 with Docz theme. You will also find a Travis configuration for automatic deployment to Github pages. 

## Add automatic deployment with Travis CI

1. Add a new Github access token here: Setting > Developer settings > Personal access tokens
1. Save your personal access token as an environment variable named `GITHUB_TOKEN`.


## Using this for user/organization page (johndoe.github.io)


If you are using automatic deployments by Travis, change .travis.yml to 

```
language: node_js
node_js:
  - "stable"
cache:
  directories:
  - node_modules
before_script:
  - "cd docs"
  - "npm install"
script:
  - "npm run test"
after_success:
  - "npm run deploy"
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GITHUB_TOKEN
  local_dir: docs/public
  target_branch: master
  keep-history: true
  on:
    branch: source
 ```
