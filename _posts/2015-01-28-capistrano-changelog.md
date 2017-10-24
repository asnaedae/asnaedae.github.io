---
title: "Capistrano changelog"
layout: post
date: 2015-01-28 18:24:00 GMT
---

### Capistrano and Changelogs

I needed a more atomic method of listing changes between two deployments whilst using capistrano, so used the following task to perform a git log between two revisions:


use the following to display:

```bash
$ cap deploy:changelog
INFO Changes between 04e7f9a and 3fd3e88 releases
INFO e7770ab Built Deployable files from Drush make
8f9d13c Built Deployable files from Drush make
3872d29 Built Deployable files from Drush make
193aaad Built Deployable files from Drush make
```

You can then of course include within any other tasks using the normal [capistrano](https://github.com/capistrano/capistrano) methods
