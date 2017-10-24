---
layout: single
title:  "Moving git repositories"
tags:
- git
---

So whilst moving between github organisations - which is relatively straight forward, I also had to move some from [Atlassian Stash](http://www.atlassian.com/software/stash) unfortunately there's not as simple a method to do this, but a good way of mirroring between two repos is as follows:

```bash
$ git clone https://donor_repo/example1 --bare
$ git remote set-url --push origin https://destination_repo/example2.git
$ git fetch -p origin && git push --mirror
```
Simples.
