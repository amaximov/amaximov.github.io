---
permalink: /2006/8/6/serendipitous-apache-tinkering
date: '2006-08-06 17:44:00'
title: >-
    serendipitous apache tinkering
---

this is something i accomplished at work in the past month that was sort
of peripheral to my "main" job. it brought this much needed sense of
accomplishment in the midst of fighting fires and dealing with
incompetence. for once i had all the people i needed close by and i had
everything i needed to get the work done.

the whole thing was merely replacing a cisco reverse proxy/ssl
termination device with an apache server. i was briefly involved in the
original solution, steering them in the right direction (sadly, pointing
a cisco consultant at their own docs to prove that they did indeed have
reverse proxy and url rewriting functionality). however this time
around, when i got involved, it turned out that the cisco device was not
able to handle the traffic altogether due to the firmware issues, so
something needed to be done in a day or two.

it was so gratifying to be able to run the whole thing to the
completion, working through firewalls/certs/nat'ting, compiling/testing
and rolling this stuff out in a matter of several hours, complete with
some quickly whipped-up load testing and monitoring. granted, it was
just a dozen internet-facing proxying sites, something i have done so
many times before, but showing the skeelz off, especially since it was
not even my job, technically, and doing it all in a few hours with all
of these folks watching, was a nice uplifting experience after long
nights of frustration beforehand.

the sad thing is that all the folks that were working on this stuff for
past three months had very little understanding of underlying technology
(and that's, of course, even worse that no understanding at all). all of
it was integration of packages into a portal and serving it via SSL to
the end user, but all they had were consultants for each of the packages
that knew only the terminology and high-level details of how their stuff
worked. so what i witnessed that night was a picture that i've seen
every single day on this project - a constantly growing school of fish
darting back and forth; as it grows in size, the movement is becoming
increasingly erratic. the primary reasons are: too many people involved,
too little people actually understanding what is going on.

but the technical reason i mention this is the fact that although apache
2.2.2 has rewritten their proxying stuff and made it much better, it has
some bizarre problems with handling connectivity with the backend server
(most likely IIS-specific) that results in the remote clients getting a
502 proxy error and the following line showing up in the error logs:

    proxy: error reading status line from remote server (null)

there are a couple of bugs filed on the apache bugzilla, but nothing
confirmed yet:

* <http://issues.apache.org/bugzilla/show_bug.cgi?id=37770>
* <http://issues.apache.org/bugzilla/show_bug.cgi?id=39499>

since my stuff was compiled with worker mpm, the easiest workaround was
to use `SetEnv proxy-nokeepalive 1`. other potential workarounds
mentioned in the bugreports are:

-   use a prefork process model as opposed to worker
-   downgrade to apache-2.0

what happens is as follows: traffic flows for a while and there are no
problems, then traffic stops for 10 minutes, then the first few requests
to hit those stale connections to the backend server get the 502 error,
without even hitting the backend server. there is nothing in between
that kills these connections, and it is not always reproducible. since i
was under time constraints, i just let it be after applying the
workaround.

another thing to keep in mind that always confuses me with the apache
reverse proxy docs: given a frontend server, and a backend server, this
is how the rules should look like:

    ProxyPass /path http://backendserver:port/path
    ProxyPassReverse /path http://backendserver:port/path

in other words, both `ProxyPass` and `ProxyPassReverse` directives have
to refer to the same server, otherwise the reverse proxy rewriting just
would not work.
