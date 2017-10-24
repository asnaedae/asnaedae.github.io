---
layout: single
tags:
  - osx
redirect_from: /shining-a-light-on-spotlight/
---

Show the status of spotlight on volumes:

```bash
$ mdutil -sa
/Shared Items/Public:
Indexing enabled.
/Volumes/Time Machine/Shared Items/Backups:
Indexing and searching disabled.
/Users:
Indexing enabled.
/Volumes/pool1:
Indexing and searching disabled.
	/Shared Items/Backups:
Indexing enabled.
	/Groups:
Indexing enabled.
```

I was recieving a few errors when trying to spotlight for applications (well they didn't appear) - running

```bash
$ sudo mdutil -i off /
Error, no index found for volume.
```
What worked to fix this for me was to move the main volume into the privacy section of spotlight and reboot (though i'd expect restarting fseventd might have the same effect) and then remove the volume from Privacy, 10 minutes later and disk has re-indexed and spotlight is working correctly.
