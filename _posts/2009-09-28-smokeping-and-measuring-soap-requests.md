---
layout: post
tags:
  - debugging
  - performance
  - smokeping
  - soap
redirect_from: /smokeping-and-measuring-soap-requests/
---

We've had an issue with performance of a SOAP interface, and here's how you
go about setting up smokeping to time it:-

```bash
extraargs = -H Content-Type:text/xml --data @/srv/scripts/soap_check/soap-test.xml
urlformat = http://server.name.com/url/soap_url
```
The only annoying problem is that the SOAP payload cannot be included as
part of the command line, so any slaves would require the file
manually copied into the same location
