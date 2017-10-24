---
layout: post
tags:
  - osx
  - file systems
redirect_from:
  - /2010/01/18/disabling-atime-on-osx/
  - /disabling-atime-on-osx/
---

Create the following plist file somewhere useful, e.g.
/Library/LaunchDaemons/com.local.noatime.plist

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
dict>
<key>Label</key>
<string>com.my.noatime</string>

<key>ProgramArguments</key>
<array>
<string>mount</string>
<string>-vuwo</string>
<string>noatime</string>
<string>/</string>
</array>
<key>RunAtLoad</key>
<true/>
</dict>
</plist>
```
Then run the following to pick up the change, or indeed, reboot:

```bash
% sudo launchctl load /Library/LaunchDaemons/com.local.noatime.plist
```

And you should now see the root file system mounted with noatime option, which should improve longevity of SSD boot drives

```bash
# mount
/dev/disk0s2 on / (hfs, local, journaled, noatime)
```
