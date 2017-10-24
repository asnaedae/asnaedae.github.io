---
layout: post
redirect_from: /node/619
---

Well there is some undocumented methods to make time machine work on non-locally attached storage, and although it might be disabled in patches - this works pretty well:

As a regular user and in a terminal

```bash
$ defaults write com.apple.systempreferences TMShowUnsupportedNetworkVolumes 1
```
Then when you visit the time machine preferences you can choose a network share as a TM location. Now it's very tempting to get a little mac mini for some zfs/nfs goodness
