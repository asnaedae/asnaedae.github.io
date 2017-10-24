---
layout: post
tags:
  - bluecoat
  - logging
redirect_from: /bluecoat-bits/
---

Suppression of authentication log entries:-

```xml
<Exception>
	exception.id=(”authentication_redirect_from_virtual_host”,
	“authentication_redirect_to_virtual_host”, “authentication_failed”)
	access_log[main](no)
```
And to get a dump of the config, though the “unencrypted” option doesn’t seem to work on SGOS 4.2.3

```bash
configure t
  line-vty
  length 0
  show version
  show status
  show configuration with-keyrings unencrypted
  length 80
  exit
  exit
  exit
```
