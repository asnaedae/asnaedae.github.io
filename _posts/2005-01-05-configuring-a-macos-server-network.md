---
layout: single
redirect_from: /2009/01/configuring-a-macos-server-network
---

So installed Leopard server over the weekend and here’s some notes and annoyances I’ve hit (and overcame)

	services fail to start – basically forward/reverse DNS must match

```bash
greebo:~ localad$ sudo changeip -checkhostname

Primary address = 172.16.10.196

Current HostName = greebo.snarc.co.uk
DNS HostName = greebo.snarc.co.uk
```

> names match. There is nothing to change.

So I cheated and am running split horizon DNS, I’ve not done the following – but is here as a reminder (and if I ever have enough disk space)

Changing clients to use your new server (running Software Update)

```bash
sudo defaults write /Library/Preferences/com.apple.SoftwareUpdate CatalogURL http://greebo.snarc.co.uk:8088/
```

And trigger an update from the command line using

```bash
$ sudo softwareupdate –install –all
```

## Time Machine

It’s just easier to start with workgroup mode and use serveradmin to run the machine without converting it.

## Things left to do:

* Network home directories
* Portable home directories
