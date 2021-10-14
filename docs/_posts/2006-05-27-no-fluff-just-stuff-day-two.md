---
permalink: /2006/5/27/no-fluff-just-stuff-day-two
date: '2006-05-27 20:50:24'
title: >-
    "no fluff just stuff" day two
---

day two started with neal ford's [talk on practical
agility](http://nofluffjuststuff.com/speaker_topic_view.jsp?topicId=270).
i feel that this is one of the areas i am lacking in - all of my daytime
job experience has happened in the environment where very few agile
practices took place. i am interested in these cookbook-like recipes
that give one a tangible feel for the steps in the process.

no revelations here, but a nice talk reaffirming the facts. his
subsequent two-part talk on sunday was far more interesting, actually
showing the artifacts produced by the project managers, and telling
real-life war stories. it turned out to be more of an introductory talk,
but some quotes did stick (or perhaps resurfaced again):

> if you are afraid of a piece of code, refactor it

> agile methods expose poor developers

> maximize the amount of work not done

> agile development is a form of risk management

in fact, risk management is probably the best selling point of agile
methodology (which neal constantly emphasized).

next was the talk by bruce tate, titled [where agile meets argyle: new
processes in established
companies](http://nofluffjuststuff.com/speaker_topic_view.jsp?topicId=176).
sadly, almost nothing there was new to me, or particularly exciting.
bruce is not an engaging speaker, compared to justin or venkat, but he
is nevertheless a very nice guy to talk to, as long as he is not in the
"speaker" mode. i really do enjoy his books and value his opinion, as
well as his drive and energy. perhaps i just heard the same arguments
over and over again throughout the whole weekend (not to mention reading
various books on the subject), so the overall impression was a bit
muted. i suppose i really never did stick up to the higher-ups, selling
agile, so some of the points seemed somewhat irrelevant to me.

a couple of times i snuck out and dropped by glenn's [talk on jvm
performance](http://nofluffjuststuff.com/speaker_topic_view.jsp?topicId=346).
in retrospect i wish i spent more time there - although most of the
subjects on paper looked like something i alerady knew (mostly through
personal performance tweaking experience on developement and admin
sides, as well as the classic java platform and java performance books),
but there were a few points that were news to me (cost of uncontested
serialization for instance). talking to him afterward i realized how
thorough and how knowledgeable he was when it came down to the innards
of java platform.

next talk was justin gehtland's [ajax
architecture](http://nofluffjuststuff.com/speaker_topic_view.jsp?topicId=297).
although i went there mostly for the entertainment value, i still got
out a lot from it - just clarifying my own understanding, and, most
importantly, learning to talk about this topic, and seeing how well he
can engage the audience. him and venkat are complimentary - venkat is a
better all-around speaker, but justin comes across a bit livelier,
filled with a sort of boyish energy and eagerly stuffing a multitude of
other topics into his talk.

talking to neal ford the night before, i was curious to see his
"[productive
programmer](http://nofluffjuststuff.com/show_session_view.jsp?sessionId=1901&showId=53)"
talk (especially since there is a book in the works, scheduled for this
fall). i stopped by a couple of times during this talk, and saw all the
right things in place - cygwin + unix + command-line tricks, scripting
languages for automation, etc. it was a good basic talk, and there was
nothing really that i learned (except reminding me the pain i felt when
i first switched from norton commander to windows95 gui).

however the topic itself warrants a longer rant, and i am really glad
neal brought it up. first of all, i make [a difference between a
programmer and a
developer](http://www.ericsink.com/No_Programmers.html). i've worked
with both kinds (and even extreme examples of both kinds), and for the
most part programmers are only useful in a big organization, coding to
the tight, verbose spec, perhaps outsourced. a developer is someone that
has a toolbox and knows when and how to use the tools at hand. i've seen
too many consultants or narrow specialists that do wonders in their
respective app development gui/ide, but freak out when it is minimized
and they face an OS in front of them, or a task that is done best with
something else (just ask me sometimes about the "laptop boy" or "tight
guys"). i used to wonder whether the knowledge of the OS and
productivity tools is important to a developer, and these days i see it
almost as a requirement, better yet - a sign of common sense. a good
argument that neal brought up - developers know more about the
underlying OS, the way it works, and the way to tweak it to maximize
their productivity.

however, there is a difference between GUI/OS productivity tricks
(shortcuts, "getting around in a hurry", note-taking apps, etc) and
development tools. both are needed, but the former is a bit tricky,
since one could use many machines, and tweaking the environment at that
point becomes painful (i myself have four machines, and i used to run
heavily customized litestep and the likes, but now i just stick to
minimal customizations: mostly firefox and cygwin + a small list of
IDEs/productivity tools). when it comes down to development tools in
one's toolbox, i want to see common sense and knowledge of a wide
variety of tools. unix background generally puts people in the right
mindselt - given the [famous "grep
question"](http://www.cabochon.com/~stevey/blog-rants/five-essential-phone-screen-questions.html)
from [stevey's list of five
questions](http://www.cabochon.com/~stevey/blog-rants/five-essential-phone-screen-questions.html),
i want to see a sensible response; and this sort of response comes from
a developer well-versed in basic unix tools.

after i switched groups at work about a year ago, i found myself in the
environment where all of a sudden i could really help less-technical
folks out by a few quick scripts - be it data imports, creating test
data, loading some stuff from LDAP, merging a bunch of spreadsheets,
etc. it is surprising how much energy is spent on these tasks, only
because there is no versatile developer around that could quickly whip
up a bunch of scripts. this is when the unix ideology really pays off -
a bunch of small tools that read stdin, print to stdout, and could be
chained together using pipes in cygwin/unix. this is when the value of a
simple `` for i in `ls *blah`; do stuff; done `` could not be
overestimated. incidentally, someone in my environment that showed a
great ability to help the folks out (not just business users, but
certified thought-leading architects) was a testing guy - a great
example of someone that can build scaffolding around a product if
needed, understands why and how stuff works - anything from OS to the
end-user product.

my personal acid test for the developer would include a few questions on
pragmatic automation - know the scripting languages, know the OS
scripting, understand when a 1000+ lines of Java code could be replaced
with a few lines of shell scripts. this is when the books like [data
crunching from pragmatic
programmers](http://pragmaticprogrammer.com/titles/gwd/index.html) and
"[pragmatic
automation](http://pragmaticprogrammer.com/starter_kit/auto/index.html)"
come in handy (but a good developer knows all that already, right?).

to conclude this rant, this is why i enjoy the "back to the unix basics"
mentality switch that was brought by the rails community.
rake/capistrano + linux/mac os x; back to the bare metal and hacking
mentality (as in building small, simple things and taking advantage of
the basic concepts, but pushing them further).

the last talk of the day was "[three technologies to
watch](http://nofluffjuststuff.com/speaker_topic_view.jsp?topicId=278)"
by bruce tate. a very anticipated topic, although he gave away some of
it during his previous talks or personal conversations. he started with
rails' active record and the way it takes advantage of metaprogramming
in ruby. i've already seen most of the talk, since [his blog entry on
the
topic](http://weblogs.java.net/blog/batate/archive/2006/01/we_should_learn.html)
was [posted on
artima](http://www.artima.com/weblogs/viewpost.jsp?thread=152273) just a
couple of months ago. great stuff nevertheless, i wish i've seen it a
year ago. next set of slides was on continuations and their
applicability in the web servers world. once again, i have already read
[bruce's article on
developerworks](http://www-128.ibm.com/developerworks/java/library/j-cb03216/index.html).
this time it made me acknowledge (once again), how much i am missing
because i am not familiar with functional languages (lisp in school and
incidental readings on haskell do not count). the idea is great, and i
am yet to grasp all the implications of it. a takeway - take a look at
continuation-based web frameworks ([rife](http://rifers.org/),
[webwork2](http://www.opensymphony.com/webwork/),
[seaside](http://www-128.ibm.com/developerworks/opensource/library/os-lightweight8/)).
finally, bruce talked about
[erlang](http://en.wikipedia.org/wiki/Erlang_programming_language), yet
again exposing my lack of knowledge about parallel systems and the math
behind it. instead of my poor interpretation of it, i will suggest
reading [yet another passionate rant by stevey
yegge](http://steve-yegge.blogspot.com/2006/03/moores-law-is-crap.html)
that talks about parallelism as it applies to CS.

the day was a bit disappointing, since a lot of the talks were based on
the blog entries i have read earlier; i guess this is the drawback of
being too close to this community and mindset. but if nothing else,
these guys are very good speakers, and it helped me to clear up a lot of
things in my head which hopefully would allow me to be a bit better at
relating this stuff to others.
