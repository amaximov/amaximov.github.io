---
permalink: /2006/2/8/and-more-cygwin
date: '2006-02-08 00:20:00'
title: >-
    and more cygwin
---

another little cygwin gem (pun intended): if your webrick starts but
outputs nothing, and never binds to a port (going through the sources
reveals that it just hangs in a backticks shell command call, but works
fine if you [run it
standalone](http://microjet.ath.cx/webrickguide/html/What_is_WEBrick.html)
without any rails stuff or pass your server script `webrick` as an
argument in command line); if you get bizarre memory relocation/unable
to remap fatal errors when running rake, then try the following:

-   shutdown/exit all your cygwin processes
-   run ash from start/run (it is under `bin\ash` in your cygwin
    directory)
-   then run `rebaseall`

this solved it for me. see [this
post](http://www.cygwin.com/ml/cygwin/2005-09/msg00967.html) for some
details.

this cygwin/rails setup is a bundle of joy, i tell you. never a dull
moment on these lovely long winter nights.
