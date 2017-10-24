---
layout: post
tags:
  - java
  - tomcat
  - nginx
redirect_from:
  - /2013/06/17/http-proxy-source-ip-and-tomcat/
  - /http-proxy-source-ip-and-tomcat/
---
Run into a situation recently where proxying applications with nginx has masked the source IP - which normally is just annoying, but with Atlassian's Crowd it's more of a problem, this can be solved in later versions (Tomcat 6.0.32+) as follows:

```xml
<Valve className="org.apache.catalina.valves.RemoteIpValve"
	internalProxies="proxy_IP_address"
	remoteIpHeader="x-forwarded-for"
	remoteIpProxiesHeader="x-forwarded-by"
	protocolHeader="x-forwarded-proto" />

<Valve className="org.apache.catalina.valves.AccessLogValve"
	directory="logs"
	prefix="localhost_access."
	suffix=".log"
	pattern="combined"
	resolveHosts="false" />
```

The following should be used within nginx to forward that data into tomcat.

```bash
proxy_set_header X-Forwarded-Proto  https;
proxy_set_header X-Forwarded-Host $host;
proxy_set_header X-Forwarded-Server $host;
proxy_set_header X-Forwarded-For $remote_addr;
```
