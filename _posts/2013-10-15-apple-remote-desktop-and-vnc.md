---
layout: post
title:  "apple remote desktop and vnc"
tags:
  - vnc
  - osx
redirect_from:
  - /apple-remote-desktop-and-vnc
  - /2013/10/15/apple-remote-desktop-and-vnc/
---
Ahh, so Apple's Remote Desktop is just a simpler implementation of the VNC protocol (I'm sure there's some propriety extensions in there but it's nice to know you can use vncclient to connect to a Mac.

Options that work well for VNC:-

```xml
[Connection]
Host=$HOSTNAME

[Options]
UseLocalCursor=1
UseDesktopResize=1
FullScreen=0
FullColour=1
LowColourLevel=1
PreferredEncoding=hextile
AutoSelect=0
Shared=0
SendPtrEvents=1
SendKeyEvents=1
SendCutText=1
AcceptCutText=1
DisableWinKeys=1
Emulate3=0
PointerEventInterval=0
Monitor=
MenuKey=F8
AutoReconnect=1
```
Not the fastest thing in the planet, but only enabling the Hextile option seems to work ok.
