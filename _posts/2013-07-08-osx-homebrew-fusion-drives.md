---
layout: post
tags:
  - file systems
  - osx
redirect_from:
  - /osx-homebrew-fusion-drives/
  - /2013/07/osx-homebrew-fusion-drives.html
  - /2013/07/08/osx-homebrew-fusion-drives/
---
There's plenty of examples of doing this already but it's as simple as:

```bash
$ diskUtil coreStorage create ssdDisk hddDisk
$ diskUtil coreStorage createVolume VolumeUUID jhfs+ "fusion Drive" 100%
```
Seems to be working so far, although with typical Apple there's no documentation on how files/objects are moved between the SSD and HDD components
