---
layout: post
tags:
  - snmp
redirect_from: /2008/09/26/argh-snmp-can-really-chafe/
---

Using version 1:

```bash
$ snmpget -c COMMSTRING -M /usr/local/share/snmp/mibs -v 1 \
	-m USAGE-MIB:PROXY-MIB:REDLINE-STATS-MIB:REDLINE-STATS-MIB:REDLINE-CONFIG-MIB \
	hostname REDLINE-STATS-MIB::sessActive.0
Error in packet
Reason: (noSuchName) There is no such variable name in this MIB.
Failed object: REDLINE-STATS-MIB::sessActive.0
```
Using version 2 (2c):

```bash
$ snmpget -c COMMSTRING -M /usr/local/share/snmp/mibs -v 2c \
	-m USAGE-MIB:PROXY-MIB:REDLINE-STATS-MIB:REDLINE-STATS-MIB:REDLINE-CONFIG-MIB \
	hostname REDLINE-STATS-MIB::sessActive.0
REDLINE-STATS-MIB::sessActive.0 = Counter64: 12247
```
Slightly annoying that - but makes certain sense
