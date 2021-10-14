---
permalink: /2008/1/1/performance-optimization
date: '2008-01-01 00:19:00'
title: >-
    performance optimization: combating the evil
---

# face the enemy

> We should forget about small efficiencies, say about 97% of the time:
> premature optimization is the root of all evil<sup>[1](#fn1)</sup>

continuing the topic of my previous post ([do not deploy black boxes,
allow for measurement, metrics, monitoring](/2007/8/24/mopping-up)), i
offer you my two rules of performance optimization (heavily *optimized*
for enterprise environment<sup>[2](#fn2)</sup>).

# rule #1: don’t do it

i’ve seen more crimes committed against software in the name of
performance optimization than for any other reason<sup>[3](#fn3)</sup>.

don’t bother with performance optimization – deliver working software
first.

instead of spending time salivating over sexy distributing caching
algorithms and debating the merits of lock striping approaches,
[implement by
feature](http://www.ayeconference.com/Articles/ImplementByFeature.html)
and most likely you will find out that performance is good enough.

a fitting quote from
[Refactoring](http://martinfowler.com/books.html#refactoring):

> The secret to fast software, in all but hard real-time contexts, is to
> write tunable software first and then to tune it for sufficient speed.

<img src="/assets/2007/11/26/runner_in_flight.jpg" data-hspace="10" data-align="right" />

i know it is hard to resist the glimmering image of a performance
superhero squeezing out a dramatic 100000x speed increase. we are all
guilty of dreaming about it. face it – you are not writing [hard
real-time
systems](http://en.wikipedia.org/wiki/Real_time#Hard_and_soft_real-time_systems).
you’ll just have to buckle up and stick to implementing business
functionality without getting to play with those exciting computational
problems.

finally, know your requirements upfront – what latency can you
*actually* tolerate, does it even matter? what throughput do you need?
make sure you have the actual numbers; both average and worst case
scenarios. guess what, in many cases it turns out that you do not need
to optimize to begin with.

after all, performance optimization is always about trade offs – leave
your options open.

# rule #2: don’t do it blindly

measure, then optimize. *most* of the software spends *most* of its time
in just a fraction of the code – the “hot spot” – find it and optimize
it away.

having a well-factored program leads to hotspots that are easier to
isolate and optimize.

way too often i see people diving in and tweaking things left and right,
just because they think they know where the problems are.

at best you will waste your time, but most likely you will actually make
things worse.

if you live in the java platform world, you are in luck – there are so
many tools out there for modern JVMs – use them!

# notes

rules are meant to be broken, but i’d rather overreact upfront to
discourage frivolous optimization.

yes, yes – you have to have basic knowledge so that you do not do stupid
things all over the place and end up bleeding to death from a thousand
cuts. luckily, in enterprise software most of these things are very
basic – a few language rules, and a few design rules – good software
developer will follow them automatically.

# why performance optimization is so alluring?

here’s my take on it – enterprise software is boring. you’ve done it a
few times, and you do not feel like cranking out the same stuff over and
over again.

<img src="/assets/2008/1/1/gloves2.jpg" data-hspace="10" data-align="right" />

so you start creating complexity to entertain yourself, to give your
mind something to chew on: you fall in love with design patterns, you
build beautiful multi-tier distributed designs with transactional
semantics all over, and you fiddle with performance optimization on
every step.

most of us have gone through it; it is like a childhood disease that you
suffer from in order to become immune. most of us survived and gained
valuable insight in the process. it does take a bit of self-reflection
and experience to realize this though.

(those that did not survive ascended to the
[stratosphere](http://www.joelonsoftware.com/articles/fog0000000018.html)
and became raving zombies – and we all know what to do with zombies).

i think the key is to understand that although enterprise software is
boring, the vast majority of all software projects still fail. this is
where the true complexity is – figuring out how to deliver working
software that customers actually use. not to mention doing it on time,
on budget, and without burning your team.

this is much harder and at the first sight a lot less sexy, but there
are still plenty of technical challenges to work through in order to
create well-engineered systems. it is just your definition of
“well-engineered” that has to change.

once you re-adjust your focus, the work is cut out for you.

it is tempting to pitch “enterprise” software against the opposite
“swing” championed by the [pragmatic
programmers](http://www.pragprog.com/),
[rails](http://www.rubyonrails.org/), and the whole community around it.
and of course, it is not the technology but the mindset.

<sup>1</sup> [donald knuth](http://en.wikipedia.org/wiki/Donald_Knuth)
paraphrasing [hoare](http://en.wikipedia.org/wiki/C._A._R._Hoare)

<sup>2</sup> with apologies to [m. a.
jackson](http://en.wikipedia.org/wiki/Michael_A._Jackson)

<sup>3</sup> with apologies to [w. a.
wulf](http://en.wikipedia.org/wiki/William_Wulf)
