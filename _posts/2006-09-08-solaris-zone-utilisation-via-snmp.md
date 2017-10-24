---
layout: single
tags:
  - solaris
  - snmp
redirect_from:
  - /2006/09/08/
  - /solaris-zone-utilisation-via-snmp/
---

It’s been a bug-bear for a long time for me that the CPU metrics when querying a Solaris 10 host are global and not zone specific (which of course makes sense, just makes it harder to track zone utilisation).

So finally wrote a basic perl script that will provide that information via a SNMP mib, output looks like the following:

```bash
> snmpwalk -v 1 -c public localhost .1.3.6.1.4.1.2021.255.7
UCD-SNMP-MIB::ucdavis.255.7.0 = STRING: "Zone name"
UCD-SNMP-MIB::ucdavis.255.7.1 = STRING: "global"
UCD-SNMP-MIB::ucdavis.255.7.2 = STRING: "gallery"
UCD-SNMP-MIB::ucdavis.255.7.3 = STRING: "nakos"
UCD-SNMP-MIB::ucdavis.255.7.4 = STRING: "mcdougallfamily"
UCD-SNMP-MIB::ucdavis.255.7.5 = STRING: "shared"
UCD-SNMP-MIB::ucdavis.255.7.6 = STRING: "packer"
UCD-SNMP-MIB::ucdavis.255.7.7 = STRING: "si"
```
Script is available at [here](....)

Current bugs/issues
> snmpwalk will not step through all the sub-trees
