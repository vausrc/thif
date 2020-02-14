---
layout: post
title:  "How to set up a custom domain on Github Pages"
date:   2020-02-10 15:27:11 +0700
categories: custom domain github
img: gh-page.png
description: # add description
tags: [Github] # add tag
---

Assuming you have already bought a custom domain (example.net) and a [Github Page](https://pages.github.com/) set up (example.github.io):

# Create a CNAME file
Create a file name `CNAME` in the project's root folder with the custom domain `example.com` inside.
```sh
# Outputs example.net to a file named CNAME
echo example.net > CNAME
```

[Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--geiyWk08--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/lpdd166ohw5e2eyd36wt.png)

You may need to configure your build command to also copy CNAME to the build folder, for example with a package.json file with React:
```json
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build && cp CNAME build/CNAME",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
```
# Configure your domain
At your domain provider (the place you bought the domain - which I recommend <porkbun.com>), find the configuration for custom host/resource records and set:
```js
Type: A
Host: @
Answer/Data/Value: 185.199.108.153
TTL: 30min (or any)
```
Do this for all 4 github page ip addresses: 185.199.108.153, 185.199.109.153, 185.199.110.153 and 185.199.111.153

You'll also need to add this one:
```js
Type: CNAME
Host: www
Answer/Data/Value: example.github.io
TTL: 30min (or any)
```
[Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--y0hVirnw--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/oewpiajem5lvoft1s7rf.png)

# Configure repository
At Github, go to the repository settings and add your custom domain in the Github Pages section.
It might take up to 24h to reflect these and/or HTTPS changes

[Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--c-ZYnmVF--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/dy4hvytp1i41ixhwk84h.png)