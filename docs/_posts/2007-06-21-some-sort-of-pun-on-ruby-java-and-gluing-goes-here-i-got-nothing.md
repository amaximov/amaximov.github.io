---
permalink: /2007/6/21/some-sort-of-pun-on-ruby-java-and-gluing-goes-here-i-got-nothing
date: '2007-06-21 14:52:00'
title: >-
    some sort of pun on ruby, java, and gluing goes here. i got nothing.
---

speaking of [gluing
things](http://blog.splitbody.com/articles/2007/06/21/its-for-gluing-things "gluing things"),
below is a [jruby](http://jruby.codehaus.org/ "jruby") script i cobbled
together to get a backup of an archaic
[snipsnap](http://snipsnap.org/ "snipsnap") instance.

as you might have guessed, it was just an excuse to play with
[ActiveRecord-JDBC](http://rubyforge.org/projects/jruby-extras/ "ActiveRecord-JDBC"),
since all it really takes is just connecting to the database and pulling
one table out.

still, it was fun and just a few lines of code, although you had to
install ActiveRecord gem as well as ActiveRecord-JDBC gem (not to
mention adding mysql jdbc driver in the classpath). as an excuse, i did
not want to deal with low-level jdbc machinery, nor did i want to
install another gem to get ruby's mysql connectivity.

although it takes an ungodly amount of time to startup, it works just
fine. here's the best of both worlds - java's jdbc type4 driver prowess
and ruby's terse and readable way of expressing yourself (plus the quick
feedback of edit-run-swear-edit cycle):

snipsnap does boast xml-rpc support, but it only provides a meager
pingback ability.
