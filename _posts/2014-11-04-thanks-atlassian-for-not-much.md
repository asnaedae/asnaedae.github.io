---
layout: post
title:  "User access with Atlassian tools"
tags:
  - atlassian
  - sql
redirect_from:
  - /2014/11/04/user-access-with-atlassian-tools
  - /articles/2014/11/04/thanks-atlassian-for-not-much.html
---
### User access times with Atlassian tools

You'd be mistaken if you had a few searches on the internet and found the following [page][1] suggesting that you could just query the application ```cwd_user``` table except when using [Crowd][2] when you should query against the crowd ```cwd_user_attribute``` table.

Unfortunately that might have been true back with [Jira][3] 4.3, although in the last few years mixing the Atlassian tools (with [Crowd][2] as SSO provider) this is no longer the case and I've found the following MySQL query works well to find out login times for each application

```sql
SELECT c.user_name AS Username,
c.email_address AS "Email Address",
from_unixtime(cua.attribute_value/1000) AS "Crowd Access",
j.updated_date AS "Jira Access",
co.updated_date AS "Confluence Access",
s.updated_date AS "Stash Access"
FROM
  crowddb.cwd_user c,
  jiradb.cwd_user j,
  crowddb.cwd_user_attribute cua,
  confluencedb.cwd_user co,
  stashdb.cwd_user s
WHERE  c.active = 'T'
AND c.user_name = j.user_name
AND c.user_name = co.user_name
AND c.user_name = s.user_name
AND cua.user_id = c.id
AND cua.attribute_name = 'lastAuthenticated'
AND DATE_SUB(CURDATE(),INTERVAL 60 DAY) >= from_unixtime(cua.attribute_value/1000)
ORDER BY 5,6,1,2;
```
And you should end up query data similar to:

```sql
+--------------+-------------------+---------------------+---------------------+---------------------+---------------------+
| Username     | Email Address     | Crowd Access        | Jira Access         | Confluence Access   | Stash Access        |
+--------------+-------------------+---------------------+---------------------+---------------------+---------------------+
| user1        | user1@example.com | 2013-04-05 10:20:30 | 2012-01-02 20:20:00 | 2013-04-05 10:20:30 | 2012-01-02 20:20:00 |
| user2        | user2@example.com | 2013-04-05 10:20:30 | 2012-01-02 20:20:00 | 2013-04-05 10:20:30 | 2012-01-02 20:20:00 |
| user3        | user3@example.com | 2013-04-05 10:20:30 | 2012-01-02 20:20:00 | 2013-04-05 10:20:30 | 2012-01-02 20:20:00 |
+--------------+-------------------+---------------------+---------------------+---------------------+---------------------+
```

[1]: https://confluence.atlassian.com/display/JIRAKB/Retrieve+last+login+dates+for+users+from+the+database
[2]: http://www.atlassian.com/software/crowd
[3]: http://www.atlassian.com/software/jira
