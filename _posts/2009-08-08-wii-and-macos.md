---
layout: single
tags:
  - osx
  - wii
  - file systems
redirect_from:
  - /2009/08/08/wii-and-maxos/
  - /wii-and-maxos/
  - /2009/08/08/wii-and-maxos.html
  - /2009/08/wii-and-macos.html
---

```bash
$ umount /Volumes/UNTITLED
$ sudo ./wbfs -p /dev/disk4s1 init
$ sudo ./wbfs -p /dev/disk4s1 df
wbfs tot:298.08G used:0.08G free:298.00G
$ sudo ./wbfs -p /dev/disk4s1 ls
wbfs empty
```
Then just use [WBFS for macos X](http://www.wehackwii.com/2009/04/darkten-has-released-native-mac-osx.html) to add in the backup images you've
created previously.
