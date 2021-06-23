# k8s-crew

[![Netlify Status](https://api.netlify.com/api/v1/badges/2d606156-0849-4bb3-be5e-0b7b08f88fc8/deploy-status)](https://app.netlify.com/sites/vigorous-euler-k8s/deploys)

![GitHub Pages](https://github.com/evilnick/k8s-crew/actions/workflows/gh-pages.yml/badge.svg)


This is the temporary blog site. There are things still to be done, but it works and is currently deployed
using netlify:  <https://vigorous-euler-k8s.netlify.app/>

It is also now configured to publish on GitHub Pages, using the generated content in the `gh-pages` branch

To add a new post, you currently need to make a new file in 

`content/en/blog/_posts/`

You can probably do this [by clicking this link](https://github.com/evilnick/k8s-crew/new/main/content/en/blog/_posts)

This should include some basic frontmatter:


```
---
title: "Hello K8s Crew"
date: 2021-04-26T11:37:04+01:00
draft: false
---

Your normal text here

## Markdown format, etc

```

If you want to test deploy yourself, just clone the repo and run:

```
hugo serve
```

then go to the link in the output.

These instructions are going to be moved to a contrib page, the README will be user-facing stuff.