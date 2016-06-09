---
layout: post
title: Using Private NPM Modules on Heroku
---

This took me a bit longer than it should have to figure out so I thought I would share what I did to get it setup. At [Treeline](https://treeline.io) we use Heroku to host a few things and we also have started using private NPM modules. When deploying these modules a custom `.npmrc` needs to be set that contains the `authToken` of a user authorized to install that module. You can read more about that on the [NPM Blog](https://docs.npmjs.com/private-modules/ci-server-config).

The main issue with using a project specific `.npmrc` that reads from an environment file is that everyone on the team must modify their shell to source their own token. This wasn't really an option for us and would be really inconvenient.

So I started looking into ways to handle this at build time. Initially I was just going to use a `preinstall` script in my `package.json` that built the `.npmrc` file and added `//registry.npmjs.org/:_authToken=${NPM_TOKEN}` as it's contents.

Unfortunately I couldn't get this to work on Heroku as it turns out they run `npm install --unsafe-perm --userconfig $build_dir/.npmrc` which at that time is too late for my changes to the `.npmrc` to take effect.

Digging through the [buildpack](https://github.com/heroku/heroku-buildpack-nodejs) I did run across the `heroku-prebuild` check though. Using this to add the project level `.npmrc` file seemed to work like a charm. Because we only want this run in production when deploying we added this script to the project:


<script src="https://gist.github.com/particlebanana/fa3fb1765aaddf40c9c37dd6e9d5d366.js"></script>

as well as the following to our `package.json`:

```
"scripts": {
  "heroku-prebuild": "node ./scripts/set-npmrc.js"
}
```

For other hosts where we use Docker containers we can just build this up in the `Dockerfile` when the image is being created. So for anyone using Heroku let me know how this works!
