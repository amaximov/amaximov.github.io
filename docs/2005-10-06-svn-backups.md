---
permalink: /2005/10/6/svn-backups
date: '2005-10-06 13:14:00'
title: >-
    svn backups
---

when backing up svn repos using `svnadmin dump -r`, first i figure out
which revision will be dumped, write a log entry and then dump
everything up to that specific revision to avoid changes that could have
been committed to the repo during that time. it turns out that if one
does not specify the range (0:$rev), the dump is created from that
revision up to the youngest, not down to rev 0 (docs explicitly say
that, but i simply missed that part). which means that with half a dozen
branches and a dozen tags a 100M repository produced a 2G dump. loading
the dump back into the repo took hours, and it was just one revision and
one transaction. half of the time loading would fail quietly altogether,
trying to commit that single 2G transaction.

once the bug in the backup scripts has been spotted, the dump is down to
200M (100M compressed) and load time is just a minute or two.
