---
permalink: /2006/8/6/solaris-8-threading
date: '2006-08-06 18:00:00'
title: >-
    solaris 8 threading
---

another quick joyous encounter: one of the co-workers was half-heartedly
beating his head for a month against a heavily-threaded java-based app
from a third-party vendor. the app ran on solaris sparc 8 and with 4-way
box it drove the sysload above 100 (!), while cpu utilization would
remain below 20% and `prstat` showed more than a thousand threads. in a
passing i asked him if he tried [alternative thread
library](http://developers.sun.com/solaris/articles/alt_thread_lib.html)
([another
reference](http://java.sun.com/docs/hotspot/threads/threads.html "another reference"))
- i have always used it for our java app servers on solaris 8, but never
saw any notable improvement, since there would be less than a hundred
threads per JVM. in this case, however, the library solved the problem -
the system load instantly dropped down to 1-2.

initially i liked M-to-M solaris 8 thread library, since its complexity
was quite sexiful to anyone studying it theoretically, but apparently a
simpler threading model is much more effective in the long run from many
perspectives, and this is why it became the default in solaris 9.
