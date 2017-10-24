---
layout: post
tags:
  - mysql
  - debugging
redirect_from: /2009/07/31/utf8-and-mysql-databases/
---

Nice bugs that no one seems to want to fix:-

```sql
mysql> create table test5 (
wibble varchar(500), PRIMARY KEY (wibble)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
ERROR 1071 (42000): Specified key was too long; max key length is 767 bytes

mysql> create table test5 (
wibble varchar(500), PRIMARY KEY (wibble)
) ENGINE=myisam DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
ERROR 1071 (42000): Specified key was too long; max key length is 1332 bytes
```
And even with MySQL 6.0.9 (using the Falcon engine which is still brand new)

```sql
mysql> create table test5 (
wibble varchar(500), PRIMARY KEY (wibble)
) ENGINE=falcon DEFAULT CHARSET=utf8 COLLATE=utf8_bin;
ERROR 1071 (42000): Specified key was too long; max key length is 1100 bytes
```
