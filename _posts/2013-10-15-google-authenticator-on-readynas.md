---
layout: post
tags:
  - hardware
  - linux
redirect_from:
  - /2013/10/15/google-authenticator-on-readynas/
  - /google-authenticator-on-readynas/
---
First I had to ensure that the stock debian packages are available for installation:

```bash
$ tail /etc/apt/sources.list
deb http://archive.debian.org/debian etch main
```
Install g++ and other dependencies

```bash
$ apt-get install g++ libpam0g-dev
```
Download google-authenticator source code:

```bash
$ git clone https://code.google.com/p/google-authenticator/
$ cd google-authenticator/
$ ./configure && make && make install
```
Then simply follow the instructions over at [here](http://www.linux.org/threads/google-authenticator-for-ssh.4590/)
