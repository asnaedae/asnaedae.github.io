---
layout: post
tags:
  - osx
  - dock
redirect_from:
  - /2008/02/07/recent-applications-window/
  - /recent-applications-window
---

This little snippet will give you a new little window for all those recent applications you launch – I seem to have picked up a habit for closing applications down when I stop working with them for an hour or two (pages etc.)

```bash
$ write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1; }; "tile-type" = "recents-tile"; }'
$ killall Dock
```
