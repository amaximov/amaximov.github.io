---
permalink: /2007/8/21/dsl-for-integration
date: '2007-08-21 03:53:00'
title: >-
    DSL for Integration
---

this is somewhat of a wide-eyed rant, but i wanted to get it off my
chest for a while.

i have worked with [Tibco
BusinessWorks](http://www.tibco.com/software/application_integration/businessworks/default.jsp)
suite of tools for quite a bit in past few years, and i came to really
appreciate it. for those not familiar with it – it is a <span
class="caps">GUI</span>-based drag-and-drop frontend that allows one to
use standard components for quickly building integration scenarios –
e.g. get data from source x, transform it, then shove it into
destination b.

for the longest time this sort of <span class="caps">GUI</span> tools
were anathema for me – i learned over time that [there is no silver
bullet](http://tinyurl.com/2ke648), [abstractions
leak](http://www.joelonsoftware.com/articles/LeakyAbstractions.html),
and for “general” software development these tools did not succeed in
addressing complexity.

at the same time Tibco BusinessWorks was remarkably successful – one
could knock out an integration scenario in under an hour and deploy it
in full enterprise glory – high availability, load balancing,
monitoring, etc, etc.

<img src="/assets/2007/8/27/toy_car.jpg" data-align="right" data-hspace="10" />

i think one way to explain that is to talk in terms of brooks’ “silver
bullet” [essay](http://tinyurl.com/2ke648) – the winning approach
addresses both *accidental complexity* (very good tools that make a
developer more productive) and *essential complexity* (focusing on a
very narrow problem domain). that is besides plain good engineering, of
course.

while *accidental complexity* is a subject for another post, it is
interesting to note how *essential complexity* was addressed by focusing
on the problem domain of integration.

generic “embrace and solve the world” tools have an unmanageable problem
domain, and it is impossible to get them right for everyone.

in this particular case it comes down to being able to express your
problem domain, define it in terms of higher-level abstractions, and
then allowing those to leak gracefully as needed.

Tibco BusinessWorks excels at integration, and the domain is very simple
– read the data, transform it, and load it elsewhere. as long as you
keep business logic to the minimum and use the tool for what it’s good
for – it shines.

at this point <span class="caps">GUI</span> is almost nothing to be
ashamed of – it is simply a representation of the abstract syntax tree
(AST) for your program – it is in a sense your integration language
represented through <span class="caps">GUI</span> abstractions. in
theory one could write a domain specific textual language to work off
the same <span class="caps">AST</span>, and it will be yet another
representation of the same thing.

[Fowler’s article on <span
class="caps">DSL</span>](http://martinfowler.com/articles/languageWorkbench.html)
i [mentioned before on this
blog](/2006/5/24/no-fluff-just-stuff-day-one-the-keynote) was very much
responsible for this redeeming outlook on <span class="caps">GUI</span>
tools.

here’s a good example – take a look at rails. it is a <span
class="caps">DSL</span> for a well-defined problem domain of small web
applications where you build the db and the app from scratch. if needed,
it leaks abstractions gracefully, falling back on the power of ruby and
metaprogramming. although it can be pushed beyond its intended domain,
its strength is in its deliberate limitations.

an emergence of [the next big
language](http://steve-yegge.blogspot.com/2007/02/next-big-language.html)
in the nearest future is perhaps just a utopia. instead it looks like
the next step is a whole bunch of languages on top of a few existing
platforms. these “smaller” languages will become more and more
domain-specific, getting us closer to the promised bliss of [intentional
programming](http://en.wikipedia.org/wiki/Intentional_programming).
their rapid adoption will build upon the strengths of a few existing
platforms.

another related term that has a nice ring to it is neal’s [polyglot
programming](http://memeagora.blogspot.com/2006/12/polyglot-programming.html).

it is really exciting to see all the stuff happening in .net and jvm
camps as they port dynamic languages to their platforms. one of the
things i am really looking forward to is all the existing “enterprise”
stuff being augmented, glued, and morphed together using these smaller,
expressive languages resulting in more “living” adaptable systems.
hopefully, this will also lead to a culture shift (and not just in the
form of apple laptops and steadily increasing enumerators prefixed with
“web”).
