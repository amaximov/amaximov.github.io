---
permalink: /2006/5/24/no-fluff-just-stuff-day-one-the-keynote
date: '2006-05-24 00:39:00'
title: >-
    "no fluff just stuff": day one, the keynote
---

the keynote is what finally delivered that "blow your mind" experience
that i was looking for. it started rather innocently with the usual
run-of-the-mill DSL talk - traditional coffee-ordering DSL, etc.
however, a little bit into it, and there was a nice distinction made
between internal DSLs and external DSLs - something I have not
articulated as clearly to myself.

internal ones are built on top of the language they are written in; they
have full access to the underlying language, but they are also bound by
its syntax and features. external DSLs is something you write a parser
for, and then either interpret or compile them. external DSLs can do
anything, at the expense of writing and maintaining a grammar (strangely
enough, JavaCC is not used as an example, although yacc and lex are (no
bison though!)), and lack of IDE support (auto-completion, color-coding,
etc). a very simple way of distinguishing the two, very nice.

next is a statement that OO is not a panacea - not everything can be
neatly modelled in hierarchies; not everything is an object. instead a
lot of problems are best modelled in a language. here i digress and
refer to another very pertinent rant by steve yegge: "[execution in the
kingdom of
nouns](http://steve-yegge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html)."
this is a very welcome approach, especially going back to functional
languages and DSLs. context is everything; the same functional language
can result in different representations, depending on the context (an
example with ruby DSL and several different includes at the top that
change its behavior).

next is something i have not thought about until now - the fact that
none of the IDEs these days work with text - it is all abstract syntax
tree (AST) that we work with. this is what allows IDEs to perform
refactorings and all kinds of other tricks. this is why IDEs used to
require one to compile the code before it could be refactored, but now
they are getting better and better at handling broken code (i.e. code
where some of the branches are missing). also, do not forget the
predecessor of all small languages - Unix shell. it would be interesting
to see where it failed, and where [microsoft
monad](http://www.reskit.net/monad/ "monad") is failing.

finally, he whipped out [JetBrains
MPS](http://www.jetbrains.com/mps/ "mps") - a tool for metaprogramming
developed by the creators of IntelliJ. it brings the power of IDE to
external DSLs - code completion, color-coding, syntax verification. in
other words, one can design their own DSLs, and have an IDE that
supports it. the tools looks very promising, although somewhat lacking
"productionalization" side. seems like the team is waiting to see what
the big boys (microsoft with [software
factories](http://msdn.microsoft.com/vstudio/teamsystem/workshop/sf/ "software factories"),
and with [intentional
software](http://intentsoft.com/ "intentional software")) will do, and
then offer an product to support it.

this leads nicely to the stuff i have been struggling with lately at
work. i do not believe in [MDA
tools](http://www.compuware.com/products/optimalj/) - any generated code
is the code one has to maintain, and [abstractions there leak very
easily](http://www.joelonsoftware.com/articles/LeakyAbstractions.html),
especially when it comes to distributed enterprise code. so the approach
to raising the abstraction level and getting closer to the problem
domain is to use terse, expressive languages. these languages could be
internal or external DSLs, as neal showed in his presentation.
alternatively, the same domain (as long as the underlying core
representation of the domain is the same AST) could be represented with
graphical tools. and this is the stuff that i do at work on a current
project - a well-defined space of enterprise integration is modeled
using simple GUI tools that include all the building blocks - queues,
web services, mappings, flow control, database connectivity, adapters to
other apps. i was uneasy at first, feeling uncomfortably close to the
MDA world, but now I can view this as yet another form of DSL.

and this leads to another topic i have been pimping left and right:
given these simple integration tools and packaged products, a typical
enterprise (the one that can be fit into the business model offered by
these packaged products and can afford them) will require a very
different type of "architect" and "developer". since it takes only a
couple of hours to knock out an integration scenario, mapping a message
from one system to another, complete with
HA/failover/load-balancing/security/etc, then majority of the work would
require less and less in-depth technical skills, but more and more of a
business knowledge. these people will know a lot more about the
business, and a lot less about computer science. granted, the breadth of
knowledge is still essential to avoid blunders, and they would be
technical people first of all, but a lot of their expertise will shift
to the business domain, once the infrastructure and packages are in
place. my favorite tabloid happens to reaffirm these sentiments in a
recent article: "[SOA predicates rise of the enterprise
architect](http://www.theregister.co.uk/2006/04/06/idc_soa/ "SOA predicates rise of the enterprise architect")".

this kind of architecture still requires a lot of technical knowledge
and developer's background, so the promise of "[situated
software](http://www.shirky.com/writings/situated_software.html "situated software")"
is still just a dream. it does, however, highlight the difference
between the developer and the architect, as well as the different
between application architect and integration architect (especially the
one that depends on business domain knowledge). my problem is that i
still enjoy developing things so much - i like building them, i like
seeing them being used by people, i like tweaking them as they run. i
like doing hands-on stuff, this is why i still do things on the side;
but i also like the challenge of developing large systems that do
require a significant domain knowledge. the question is whether my
current occupation is indeed a domain that i am interested in knowing
more about.

in retrospect, i think a lot of the talk came from martin fowler's
article on [language
workbenches](http://www.martinfowler.com/articles/languageWorkbench.html),
which follows the same general layout as neal's talk (neal also quotes
fowler quite a lot, but then who doesn't? the man deserves it; i just
wish i had a better memory). in any case, the talk was excellent, and i
am looking forward to digging more into this topic.

the whole keynote is available on [neal's
site](http://www.nealford.com/#recent_confereces):
[slides](http://www.nealford.com/downloads/conferences/2006_nfjs_canonical/Neal_Ford-Language_Oriented_Programming_Keynote-slides.pdf "slides"),
[samples](http://www.nealford.com/downloads/conferences/2006_nfjs_canonical/Neal_Ford-Language_Oriented_Programming-samples.zip "samples")
