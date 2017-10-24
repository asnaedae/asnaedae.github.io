---
layout: post
redirect_from: /wiki/Troubleshooting
---

Error:

```xml
Internal error: There was a database error: \
java.security.AccessControlException: access denied \
(neo.xredsys.auth.UserPermission 1 create)
```
Solution: You've not followed the installation instructions and not changed the java.security settings:

```xml
-Djava.security.policy=/u01/apps/escenic/engine-4.3-2/security/java.policy
-Djava.security.auth.login.config=/u01/apps/escenic/engine-4.3-2/security/jaas.config
```
