---
layout: single
tags:
  - solaris
  - mercurial
  - dsvn
redirect_from: /playing-with-mercurial/
---

Well, been playing with opensolaris and they use mercurial as a DSVN - and another benefit of that over git is that the command set is very much similar to SVN/Subversion - which is important for us people who /don't/ use it every day.

Migrating was straight-forward:

```bash
$ mkdir ~/svn && cd ~/svn
$ hgimportsvn https://dubdubdub.co.uk/svn/mike
$ find . -name .svn -type d | xargs rm -rf
```
One thing to note when using - which took me a bit of reading to realise - it's distributed, so if you've your own local copy - you have to commit and then push/pull changes out!
