---
layout: single
tags:
  - java
  - debugging
redirect_from:
  - /2010/07/07/jmx-and-firewalls-or-how-to-hate-rmi-slightly-less/
  - /2010/07/jmx-and-firewalls-or-how-to-hate-rmi-slightly-less
---

So at least with Java 1.6 the JVM can use SOCKS for proxying RMI requests, so
to get the wonderful jvisualvm (think 1.5 visualGC) working use the following
incantations. This requires the initial RMI registry port is open to the client.
First the initial SSH to server enabling the SOCKS tunnel

{% highlight bash %}
$ ssh -D localhost:9696 servername
{% endhighlight %}


And now for jvisualvm:

{% highlight bash %}
$ jvisualvm \
  -J-Dnetbeans.system_socks_proxy=localhost:9696 \
  -J-Djava.net.useSystemProxies=true
{% endhighlight %}

props to [Stackoverflow](http://stackoverflow.com/questions/1609961/visualvm-over-ssh) for the hints
