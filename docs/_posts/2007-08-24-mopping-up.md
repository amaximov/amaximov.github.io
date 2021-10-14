---
permalink: /2007/8/24/mopping-up
date: '2007-08-24 21:51:00'
title: >-
    mopping up
---

this is a rant, inspired by working in both developer and admin roles
over the years (i strongly believe in “eating your own dogfood” when it
comes to building and running the apps, but this is a whole different
topic).

my experience is that given a choice of manageability/logging/monitoring
vs. extra performance i will always choose the former. the amount of
time spent troubleshooting performance and stability issues on live
application in production trumps any hardware (and sometimes even
development) costs.

so instead of satisfying [your inner
ricer](http://www.urbandictionary.com/define.php?term=Ricer) and
deploying a highly-performing black box hotrod, spend the time to put
the probes in, make it declaratively manageable; if your OS/hardware
provides any sort of isolation and partitioning – consider it; take
advantage of existing platforms and tools.

<img src="/assets/2007/8/27/jet_train.jpg" data-align="right" data-hspace="10" />

take [Tibco
BusinessWorks](http://www.tibco.com/software/application_integration/businessworks/default.jsp)
for instance. besides having their own suite of monitoring/management
tools they allow (perhaps serendipitously) individual “worker engines”
to be deployed in separate JVMs (which could be on different machines)
so you can analyze and manage them using not only an existing ecosystem
of Java tools, but also fall back on your regular OS tools – per-user,
per-process, per-box.

the benefit of this simplicity becomes obvious once you have worked with
apps that insist on packing everything into one <span
class="caps">JVM</span> – worker engines, daemon-like processes,
queuing, etc, etc. management and tuning becomes a nightmare; on a
flipside it is guaranteed job security and high salaries.

so what can a developer do? besides the obvious, consider an api to talk
to your application and tweak it as it is running (look at [those ol’
smalltalk
dudes](http://blog.jonudell.net/2007/05/21/a-conversation-with-allen-wirfs-brock-about-the-history-of-smalltalk-and-the-future-of-dynamic-languages/)),
or better yet – a command-line scriptable console that exposes your
app’s domain. here’s props to [bea](http://www.bea.com/) folks – their
flagship server product for years had a python
([jython](http://www.jython.org/) to be exact)-based
[console](http://tinyurl.com/36zjeq) that allowed one to connect to a
running cluster and make changes to it on the fly. [similar
functionality](http://wiki.rubyonrails.org/rails/pages/Console) is
provided by [rails stack](http://rubyonrails.com/), although technically
you only get connectivity to the database, not the actual running
application instance. still, it is a big step.

another tip of the hat in bea’s direction – [their <span
class="caps">JVM</span>](http://tinyurl.com/3cvzus) for years had
*actually usable* manageability tools; sun was late, and even when they
started delivering them, the tools were really clunky (i am still
waiting for something similar to
[jrcmd](http://edocs.beasys.com/jrockit/geninfo/diagnos/ctrlbreakhndlr.html)
tool from sun that allows me to do simple things like collecting
threaddumps from a jvm on all platforms, including windows and
redirecting them to a given file, since jvm might be running with stdout
sent to /dev/null). bea’s [mission
control](http://dev2dev.bea.com/jrockit/tools.html) has been around for
a while in various forms – i want to be able to attach to my production
<span class="caps">JVM</span> and look at <span class="caps">GUI</span>
representation of memory distribution, object counts, stack traces, heap
info; but on top of that it gives me an ability to explore and act upon
exposed <span class="caps">JMX</span> beans both from the <span
class="caps">JVM</span> and the app, set up triggers and alerts that
start recordings, memory dumps, send emails, etc. this becomes
indispensable, especially for hand-me-down apps or third-party software.

this is actually a big change in mentality – gradually people are
realizing that they should be able to monitor stuff in production, live,
as it is running. hence we have things like (under appreciated)
[dtrace](http://www.sun.com/bigadmin/content/dtrace/), and more and more
investment into the platforms that support that sort of runtime
lightweight dynamic analysis. these days it is expected that apps should
be on 24/7, and ability to dynamically redeploy things, reconfigure
things, analyze things is crucial.

finally, i have seen way too many folks that consciously refuse to learn
about how their code runs – the minimum about the OS, the network, the
tools, the tuning. i am willing to consider and understand, as long as
they have those that *do* know around. sadly, too often this
responsibility gets shifted to the OS admins that could not care less.

all sorts of disclaimers apply – in many cases the apps are so small
that one can pile them together and forget about them. the apps that
will benefit most from the manageability stuff mentioned above are the
ones that churn through a lot of data and have pretty strict
uptime/latency requirements. in addition, it is assumed that there are a
lot of people working on them, so tools and approaches should be
somewhat uniform.
