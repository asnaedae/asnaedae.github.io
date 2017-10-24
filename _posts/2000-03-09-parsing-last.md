---
layout: single
title:  Parsing last log /var/log/wtmp
tags:
- unix
---

```
#!/bin/sh

# total_logged_in - parses ``last'' ouput to something more sensible.
# if you give it a parameter, it will only display last information for
# that user

last $1 | 
nawk '
{
	if (NF = 10 && $10 != "in") {
		gsub(/\(/, "", $10);
		gsub(/\)/, "", $10);

		split($10, a, ":")
		if (split(a[1], b, "+") == 1) {
			mins=(a[1]*60+a[2])
			user[$1] += mins
			entry[$1]++
		} else {
			mins=(b[1]*1440+b[2]*60+a[2])	
			user[$1] += mins
			entry[$1]++
		}
	}
}

END {
        printf("Person   \t<DD:HH:MM>\Total Con\n")
	print  "==========================="

        for ( person in user ) {
                mins = user[person]
                nohours = int(mins/60)
                mins -= nohours*60
                nodays = int(nohours/24)
                nohours -= nodays*24
                printf("%-10s <%.3d:%.2d:%.2d>\t%.4d\n", 
		person, nodays, nohours, mins, entry[person])
        }
}
'
```

