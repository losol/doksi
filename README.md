# Doksi - documentation template

A starter for adding documentation as code to a project. This documentation template is built on Gatsby v2 with Docz theme. You will also find a Travis configuration for automatic deployment to Github pages. 

After creating a new repository you will need to update the `/docs/package.json` file with links to your own repository: 

```
  "repository": {
    "type": "git",
    "url": "https://github.com/yourusername/doczy"
  },
  "bugs": {
    "url": "https://github.com/yourusername/doczy/issues"
  }
```

## Add automatic deployment with Github Actions
Take a look on the sample workflow for adding automatic deployments.

## Add automatic deployment with Travis CI

1. Add `.travis.yml`
1. Add a new Github access token here: Setting > Developer settings > Personal access tokens
1. Save your personal access token as an environment variable named `GITHUB_TOKEN`.


## Using this for user/organization page (johndoe.github.io)

Have the source code in the source branch, as github uses the master branch for serving user/organization page.

```sh
git branch -m source
git push -u origin source
```

Install github pages: `npm install gh-pages --save-dev`

Add a script to deploy pages in package.json: 
```
    "scripts": {
        "deploy:githubpages:org": "gatsby build && gh-pages -d public -b master",
    }
```

To deploy, just run `npm run deploy:githubpages:org`.

If you are using automatic deployments by Travis, change .travis.yml to 

```
// code omitted for brevity
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

## Thanks

With inspiration from 
 * [How we switched to documentation-as-code with Gatsby.js and Netlify — Markdown & hosting](https://medium.com/squadlytics/how-we-switched-to-documentation-as-code-with-gatsby-js-and-netlify-part-1-2-1f57ad732a05)
 * [Gatsby docs: How Gatsby Works with GitHub Pages](https://www.gatsbyjs.org/docs/how-gatsby-works-with-github-pages/)
 * [Travis CI docs: GitHub Pages Deployment](https://docs.travis-ci.com/user/deployment/pages/)

