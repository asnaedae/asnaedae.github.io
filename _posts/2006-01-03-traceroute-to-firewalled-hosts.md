---
title: Tracing firewalled hosts
layout: single
category:
tags:
  - networking
published: true
---

Nice little tool called [tcptraceroute](https://github.com/mct/tcptraceroute), just uses TCP
syns instead of ICMP/UDP to give you a more meaningful traceroute;
still relies on ICMP time exceeded messages, but still, every little
helps when trying to debug someone elses problem!



