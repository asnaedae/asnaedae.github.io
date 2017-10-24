---
layout: single
title:  "CentOS/RHEL 7"
tags:
  - redhat
#redirect_from: /2014/10/13/centos-7
---

So after many years the following changes I've so far run into with CentOS 7

### firewalld

```bash
# firewall-cmd --zone=public --add-service=https
success
# firewall-cmd --zone=public --add-service=http
success
```

```bash
# firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: eth0 eth1
  sources:
  services: dhcpv6-client http https ssh
  ports:
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:
```

### systemd

```bash
# systemd enable nginx
# ln -s '/usr/lib/systemd/system/nginx.service' '/etc/systemd/system/multi-user.target.wants/nginx.service'
```

```bash
$ systemctl status nginx
nginx.service - nginx - high performance web server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled)
   Active: active (running) since Tue 2014-10-14 08:19:32 UTC; 1 day 3h ago
     Docs: http://nginx.org/en/docs/
...
```
