---
layout: single
tags:
  - snmp
redirect_from:
  - /2009/10/snmp-over-ssh-tunnels.html
  - /snmp-over-ssh-tunnels/
---

Sometimes you just need to tunnel UDP based protocols - such as SNMP - and the easiest ways is to use socat

```bash
$ socat tcp4-listen:6667,reuseaddr,fork UDP:DESTINATION:161
$ socat udp4-listen:161,reuseaddr,fork tcp:localhost:6667
```
And in combination with your normal SSH tunnel

```bash
$ ssh -L6667:localhost:6667 BASTION_HOST
```
