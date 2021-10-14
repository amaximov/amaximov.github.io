---
permalink: /2008/9/19/concurrency-part-2-actors
date: '2008-09-19 11:59:00'
title: >-
    concurrency: part 2 - actors
---

-   [part 1](/2008/9/12/concurrency-part1)

# message-passing

<img src="/assets/2008/9/19/horn.jpg" data-align="right" data-hspace="10" />

if [shared memory makes concurrent programming
difficult](/2008/9/12/concurrency-part1), what else is there that an app
developer can use?

one way of representing coarse-grained parallelism is through
*message-passing concurrency*.

the idea is pretty simple – the only way to share state between isolated
components is through message passing. what happens inside the
components, is their own business.

there is no global state of the whole system, unlike in shared memory
program that behaves like a giant state machine. sending and receiving
of messages happens concurrently together with the computations by the
components themselves. this approach is much easier for the developer to
reason about and it maps easily to multiple CPUs and multiple machines.

a lot of the enterprise workflow-like processing falls into this model.
it is basically a pipeline of worker pools, configured independently and
possibly running on separate machines. a unit of work travels through
the pipeline, as it is being handed off from one set of workers to
another.

# actors

<img src="/assets/2008/8/25/norma.jpg" data-align="right" data-hspace="10" />

one of the common implementations of message-passing concurrency is
[actor model](http://en.wikipedia.org/wiki/Actor_model). i’ll take a
liberty to interpret this model to fit my own developer needs, even
though i am butchering decades of academic research in the process.

actors model represents well multiple computers talking to each other
using network packets, components exchanging messages using <span
class="caps">JMS</span>, independent processes or threads talking to
each other using messages – basically anything where isolation is
possible and interactions are loosely coupled.

usually each actor has a *mailbox* associated with it (often represented
with a queue), where messages are stored until an actor processes them.
messages map well to physical artifacts in the real world – they are
immutable, and only one actor can handle a given message at a time.

actors are connected with *channels*; individual actors are isolated
from each other – a failure of an actor does not affect another actor.
no other actor can change the inner state of a given actor – the only
way to communicate is through message-passing.

messaging is usually asynchronous, but synchronous messaging could also
be useful.

depending on implementation, beware of deadlocks if you are using
synchronous messaging. another issue to keep in mind is order of
messages – depending on implementation it might not be preserved.

while some advocate “everything is an actor” approach, and I get dizzy
imagining the possibilities, the pragmatic app developer in me is living
in the real world among existing apps. in this case actors work best as
a library for the existing language.

### erlang

although i shied away from “actors everywhere” approach above,
[erlang](http://www.erlang.org/) is the most successful implementation
that actually does just that. it is not just the language, but a whole
platform that transparently runs actors within a single process as well
as across multiple machines.

as this topic is heating up, one should at least [read the
book](http://www.pragprog.com/titles/jaerlang/programming-erlang) and
play with the language. after all, *a language that doesn’t affect the
way you think about programming is not worth knowing*, and erlang is
enough of a paradigm shift to kickstart your concurrency thinking.

### Tibco BusinessWorks

as i’ve [described before](/2007/8/21/dsl-for-integration),
BusinessWorks (BW) is an example of an integration [<span
class="caps">DSL</span>](http://en.wikipedia.org/wiki/Domain_Specific_Language)
that happens to use actors.

given an integration *process* (e.g. receive a message on <span
class="caps">JMS</span> queue A, enrich it from a database, transform
it, and send it to a <span class="caps">JMS</span> topic B), you
describe it using BW language constructs. then it becomes an actor
*definition* that you can deploy on an *engine* (really a managed <span
class="caps">JVM</span> instance). there could be multiple engines
running on multiple machines, and each engine can have many process
*instances* (aka *actors* in our terminology) running inside of it. a
process *instance* gets created from a process definition whenever a new
message arrives on a queue (*mailbox* in actors’ terminology).

a scheduler inside the individual engine takes care of creating process
instances (there could be thousands) and scheduling them on the worker
threads.

all of this mapping happens at deploy time, as a developer you do not
worry about it.

actors talk to each other using message-passing, thus your actor
implementation does not even have to worry about threads or concurrency
– you just express your integration logic. you could use shared memory,
but it would not scale well, since you are limited to one <span
class="caps">JVM</span>; nor would it be natural, since you have to use
explicit language constructs; this language support for immutability is
very convenient, as i have [mentioned
earlier](/2008/9/12/concurrency-part1)

if you use a <span class="caps">JMS</span> server to pass messages
around, it becomes a sort of a *mailbox*, holding messages for you in
the queue. each incoming message would eventually spawn an instance of
the actor, feeding it the message as an argument. multiple instances of
the same actor can read from the same queue, thus achieving
load-balancing.

once you recall that jms supports ~~-filters~~- *selectors* you have the
actors implementation that curiously matches something like
[erlang](http://www.erlang.org/)

note that this is not fine-grained parallelism; your units of work are
more coarse-grained and very loosely coupled, but fundamentally, the
model is the same, and it scales like crazy achieving massive
throughput.

even if you do not end up using BW, you can implement this model by hand
relatively easy.

so what if i wanted more fine-grained and more efficient support for
actors in my language of choice (provided i am not using
[erlang](http://www.erlang.org/))?

### ruby

[revactor](http://revactor.org/) networking library includes actors
implementation (also see [this great intro to
actors](http://revactor.org/philosophy) by Tony Arciery), but i have not
seen a more generic approach yet.

note that ruby is really hampered by lack of proper threading support;
this is why [jruby guys](http://jruby.codehaus.org/) are in a much
better shape if they were to roll their own actors implementation.

### scala

this is probably the most mature implementation i’ve seen (see [this
paper](http://lamp.epfl.ch/~phaller/doc/haller07actorsunify.pdf)). they
take advantage of scala language features to simplify the syntax and
unify synchronous and asynchronous message-passing. individual actors
are represented as threads or more light-weight primitives that get
scheduled to run on threads in the thread pool. it is type-safe, but it
relies on convention to make sure you do not mutate your messages.

although i could see where representing actors as threads could be too
heavyweight for some tasks, in the case of java and scala, your mileage
may vary (see [this
presentation](http://www.classhat.com/tymaPaulMultithread.pdf) from Paul
Tyme).

### groovy

given language features like closures and general simpler syntax,
together with the fact that it sits on top of <span
class="caps">JDK</span> that includes `java.util.concurrent`, one would
imagine that [groovy](http://groovy.codehaus.org/) would be a perfect
candidate for actors implementation. however, the only thing i found so
far was [groovy actors](http://www.groovyactors.org/), and it seems to
have been dormant for a while.

### python

i do not know enough about python’s memory model and its implementation,
but i suspect is suffers from the same “feature” as ruby – i.e. global
interpreter lock, which means that it won’t be able to scale to multiple
CPUs (and, similar to ruby, [jython](http://www.jython.org/Project/)
that builds on <span class="caps">JVM</span> comes to the rescue).

the only thing i’ve looked at so far is [stackless
python](http://www.stackless.com/), which is a modified version of
python that makes concurrency easier (see [this
tutorial](http://members.verizon.net/olsongt/stackless/why_stackless.html)
by Grant Olson that also includes actors). it introduces *tasklets* aka
fibers, channels, and a scheduler among other things.

### java

this is where i am a bit surprised – i do not see a good
drop-in-a-jar-and-go actors library blessed and used by all. there seems
to be some research projects out there, but i want something that works
for me now and supports in-memory zero-copy message passing, sync/async
messaging, and type safety. i am OK with abiding by conventions instead
of compiler checking things for me.

i suspect that the reason for this is the fact that some rudimentary
form of actors can be implemented relatively easy using existing
concurrency libraries, and this approach is intuitive without putting
labels on it.

nevertheless, this is what i found:

-   [jetlang](http://code.google.com/p/jetlang/) is a port of a .NET
    library and looks at Scala actors for inspiration. it is still quite
    beta, but it looks promising
-   [kilim](http://www.malhar.net/sriram/kilim/) (from one of the
    principle engineers of weblogic server) still seems to be a bit too
    much of a research project for my taste, but the theory behind it is
    sound

and there is a number of research projects out there:

-   [<span
    class="caps">SALSA</span>](http://wcl.cs.rpi.edu/salsa/ "Simple Actor Language System and Architecture")
-   [functional java](http://functionaljava.org/) contains actors
    implementation; see [this blog
    entry](http://blog.tmorris.net/actor-concurrency-for-java/) as well
    as [this
    one](http://apocalisp.wordpress.com/2008/07/28/threadless-concurrency-with-actors/)
    for examples
-   [Communicating Sequential Processes for
    Java](http://www.cs.kent.ac.uk/projects/ofa/jcsp/ "JCSP")

# bottom line

actors is a great abstraction, and “good enough” version of it is easy
to implement – think about it, consider it, use it!

it helps if your language/platform supports concurrency primitives to
build upon. this includes true threading support that scales to many
CPUs, although we could also benefit from a standard
[fibers](http://en.wikipedia.org/wiki/Fiber_%28computer_science%29)
implementation, since they are more lightweight than typical threads and
would allow creation of a large number of actors that later could be
mapped onto threads for execution.

each language could benefit from a well thought-out actors library,
since it would push developers in the right direction.

it is not right for everything though – it might not be fine-grained
enough, it might not map well to problems that rely on ordering of
messages or presence of any other state across multiple actors or
multiple messages.

# to be continued

what is on the horizon that is worth noting? what are some of the
interesting research topics? what have we forgotten over the years? what
other heuristics/patterns and libraries could be immediately useful?

-   [part 1](/2008/9/12/concurrency-part1)
