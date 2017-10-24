---
layout: post
tags:
  - java
  - debugging
redirect_from: /2010/06/30/java-log-files/
---

So debugging java can be a mighty pain, a little few lines of ways to make
it simpler.

```bash
# grep -m 1 -n '^2010-06-30 14:20:' catalina.out
11746233:2010-06-30 14:20:01,011 DEBUG com.beginning.of.line
# grep -m 1 -n '^2010-06-30 14:21:' catalina.out
11747788:2010-06-30 14:21:00,161 WARN org.apache.commons.httpclient.HttpMethodBase - Going to buffer response body of large or unknown size. Using getResponseBodyAsStream instead is recommended
# sed -n '11746233,11747788p' < catalina.out
```

This gives start line and end line between any two greps and then the body of the log file from those two lines.
