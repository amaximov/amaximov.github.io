---
permalink: /2005/10/3/powered-by
date: '2005-10-03 23:51:00'
title: >-
    powered by
---

perhaps it is my vanity to blame for having chosen to run the blog
software myself; of course this is an opportunity to waste an enormous
amount of time tweaking the blog engine and themes, instituting a backup
schedule, installing updates, fighting bugs - precisely what I have been
doing with [typo](http://typo.leetsoft.com/).

I've chosen typo over [wordpress](http://wordpress.org/) and
[mt](http://www.sixapart.com/movabletype/), since I wanted to play with
[rails](http://www.rubyonrails.com/) (and what blog-aware netizen is not
guilty of drinking the kool-aid these days?). obviously it is still very
much a beta software - I've spent a few hours trying to install it under
www.domainname.com/blog, finally throwing in the towel and resorting to
blog.domainname.com setup; the sidebar admin interface is buggy, not
remembering the values, or populating them with defaults like "feed" and
"null"; same goes for the comment posting interface under IE; not to
mention that it is crazy resource pig - [fcgi](http://www.fastcgi.com/)
and all, it takes a few seconds to generate a non-cached page (I bet it
is something to do with restarting processes and cgi and rails startup
slowness in general - but I have not looked at it in details yet). oh
and despite their oh-so-smug note, do not use trunk - a flurry of
migration commits this weekend was a good lesson.

so now it is just a matter of time - either the newness wears off,
pragmatism takes over and I switch to a proven platform, or typo matures
enough to be usable.

it is a cute toy, buzzword-compliant, and still shiny and new to justify
spending the time playing with it. I should try and track down a bug or
two, to make up for all the bile in the paragraphs above.

i am yet to find out what kind of syntax it supports for the posts (it
better not be a subset of straight html), useful wiki-like macros,
uploading images, etc.
