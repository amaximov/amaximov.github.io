---
permalink: /2009/1/29/public-enemy-no-1
date: '2009-01-29 04:33:00'
title: >-
    Public Enemy No.1
---

[Alex Miller aka Pure Danger Tech](http://tech.puredanger.com/) has [a
great
entry](http://tech.puredanger.com/2009/01/27/java-concurrency-bugs-mutable-statics/)
on most common concurrency bugs.

the timing is perfect – this very thing bit me today. long story short,
an old app, previously perceived to be multi-threaded, was recently
converted to actually be multi-threaded, and then, once traffic ramped
up a bit, exhibited peculiar behavior when perfectly good dates could
not be parsed. thank god it blew up, as opposed to quietly corrupting
the data.

so something as innocent-looking as
`private static final SimpleDateFormat` declaration was the culprit:
[`java.text.DateFormat`](http://java.sun.com/javase/6/docs/api/java/text/DateFormat.html)
is not thread-safe.

luckily, it is easy enough to spot and reproduce (`threadPoolSize` and
`invocationCount` in [TestNG](http://testng.org/) simplify it even
further).

a pessimist would heave a mighty sigh, once again swear on the copy of
[<span
class="caps">JCIP</span>](http://www.javaconcurrencyinpractice.com/) to
find and root out every frivolous `static` out there with the help of
[FindBugs](http://findbugs.sourceforge.net/bugDescriptions.html#STCAL_INVOKE_ON_STATIC_DATE_FORMAT_INSTANCE)
or a simple regex.

meanwhile, there is
[joda-time](http://joda-time.sourceforge.net/faq.html#threading) and a
promise of [jsr310](http://jcp.org/en/jsr/detail?id=310)

but of course this whole experience still leaves you feeling cheated and
dirty – why, god, why?! something so function-like and stateless in
nature insists on stowing things away.
