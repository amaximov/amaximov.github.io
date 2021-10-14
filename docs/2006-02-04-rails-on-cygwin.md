---
permalink: /2006/2/4/rails-on-cygwin
date: '2006-02-04 18:55:00'
title: >-
    rails on cygwin
---

finally it works out of the box: update cygwin, run "`rails blah`", then
"`cd blah`" and "`script/server`" and voila! ruby 1.8.4 and rails-1.0.0
\*gasp\*

well, now if you *really* want to use it, you also need to fix
incompatibilities of rails-1.0.0 with rake-0.7.0, so cd into
`/usr/lib/ruby/gems/1.8/gems/rails-1.0.0` and run
"`` for i in `find . -type f`; do grep inline-source $i && echo $i; done ``"
and fix all occurrences of \<\< 'option option' with \<\< 'option' \<\<
'option'.

but that's just details, right? who cares about those little things? oh
the joy!
