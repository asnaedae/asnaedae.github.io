---
layout: single
tags:
  - f5
  - bigip
  - irules
---

A little video, thin on detail of course, but hints at some home truths on building/designing scale-able applications (and i’d go so far to say that they are applicable to ALL applications not just webapps)

![Building Scaleable Rails Apps](http://joyent.vo.llnwd.net/o25/videos/LinkedIn-Bumpersticker-LED-Scaling-Rails.m4v)

Of course, I know Ben Rockwood like’s his solaris and F5′s – but that’s not going to surprise many (and I just LOVE f5s)

And here’s a blog entry with the details on /how/ that’s done:-

[FBRef and iRules](http://www.joyeur.com/2008/04/18/the-wonders-of-fbref-and-irules-serving-pages-from-facebooks-cache)

. . . basically as simple as:-

```tcl
when HTTP_REQUEST {
	if { [HTTP::uri] contains "/popular_something/list"} {
		HTTP::respond 200 content "<fb:ref handle='[HTTP::uri]'/>"
	} else {
		pool facebook.application_server_pool
	}
}
```
