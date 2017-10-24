---
layout: post
title:  "Crowd logged in users"
tags:
  - atlassian
  - sql
redirect_from:
  - /2014/04/03/atlassian-crowd-and-last-logged-in-users/
  - /atlassian/crowd/sql/2014/04/03/atlassian-crowd-and-last-logged-in-users.html
---
This came in useful for me today to understand users that could be disabled from a [crowd](http://www.atlassian.com/software/crowd) instance:

```sql
SELECT cwd_user.user_name AS Username,  
cwd_user.email_address AS "Email Address",  
from_unixtime(cwd_user_attribute.attribute_value/1000)  AS "Last Logged In"
FROM cwd_user
LEFT OUTER JOIN cwd_user_attribute ON cwd_user_attribute.user_id = cwd_user.id
AND cwd_user_attribute.attribute_name = 'lastAuthenticated'
WHERE  active = 'T'
ORDER BY 3,2,1 ;
```
