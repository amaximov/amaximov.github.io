---
permalink: /2008/9/12/concurrency-part1
date: '2008-09-12 09:10:00'
title: >-
    concurrency: part 1
---

true to the [purpose of this blog](/2005/10/2/hello-world-readme), below
is an attempt to organize my (admittedly very superficial) experience
with concurrency.

-   [part 2](/2008/9/19/concurrency-part-2-actors)

# my 10GHz <span class="caps">CPU</span>

<img src="/assets/2008/9/12/10ghz.jpg" data-align="right" data-hspace="10" />

you probably noticed that [moore’s
law](http://en.wikipedia.org/wiki/Moore%27s_Law) does not really apply
anymore when it comes to <span class="caps">CPU</span> speed. if it were
holding up, we would have had 10GHz CPUs by now, but for half a decade
we haven’t really moved past 3GHz.

that is to be expected for the current generation of hardware – the
gains have to happen elsewhere. for a little while we’ll get performance
boost due to increase in size and speed of the caches that would improve
[locality](http://en.wikipedia.org/wiki/Locality_of_reference), but in
the long run it seems that multiple CPUs is where the improvements are
to be mined from (this also includes specialized CPUs like
[Cell](http://en.wikipedia.org/wiki/Cell_microprocessor) and
[GPUs](http://en.wikipedia.org/wiki/Graphics_processing_unit) in
general).

this means that more and more people will have to think about their
applications in terms of parallel processing. this also means that
optimizations will become more and more important for those workloads
that cannot be parallelized and therefore will be stuck on a single
<span class="caps">CPU</span> (for a good introduction see [The Free
Lunch Is Over](http://www.gotw.ca/publications/concurrency-ddj.htm) at
Dr. Dobb’s Journal).

the bottom line is that as an app developer you cannot ignore the
problem any longer; to make matter worse, there is no automagical
solution in the nearest future that would make your application take
advantage of multiple processors.

# my concurrency story

in past decade most of the stuff i’ve worked with had some sort of
coarse-grained parallelism; the rest was taken care of by the underlying
framework.

i started with a unix philosophy of small programs connected via pipes,
each performing a simple task. a little later came in `fork` and
signals. things were simple, and OS took care of everything.

then came the web – it was mostly stateless with the database doing all
the heavy lifting when it came to shared state. we just added boxes if
we needed to grow. in [<span
class="caps">ETL</span>](http://en.wikipedia.org/wiki/Extract,_transform,_load)
multi-box, multi-cpu setup was also natural, and the tools were designed
to conceal concurrency; same goes for
[integration](http://en.wikipedia.org/wiki/Enterprise_application_integration),
where concurrency was at the level of data flows, which made things
rather simple.

it is only in the past year or so when i had to really dive in deeper
into relatively low-level concurrent development with java.

<img src="/assets/2008/8/25/jcip.jpg" data-align="right" data-hspace="10" />

my [dog-eared copy](http://techbus.safaribooksonline.com/0321349601) of
[Java Concurrency in
Practice](http://www.javaconcurrencyinpractice.com/) has proved to be
quite an indispensable reference. the book is a bit uneven, and the
editor should have spent more time on it, but you get used to it. it is
a great practical resource, especially in the presence of so much
confusing and incomplete information online.

[jsr-166](http://gee.cs.oswego.edu/dl/concurrency-interest/index.html)
introduced in java5 (and the primary subject of the book) is such a
productivity boost; being a part of <span class="caps">JDK</span>, it is
a big step forward towards letting mere mortals like me really embrace
concurrent programming.

i find myself using
[Executors](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/Executors.html)
convenience methods all the time: it is so easy to create a pool, and
then just feed it
[Callable](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/Callable.html)
instances, getting a
[Future](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/Future.html)
instance as a handle in return. if more flexibility is needed, i use
[ThreadPoolExecutor](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/ThreadPoolExecutor.html).
[Queues](http://java.sun.com/j2se/1.5.0/docs/api/java/util/Queue.html)
are great as a communication channel for any sort of producer/consumer
scenario, anything that requires message-passing or any sort of other
work hand-off.
[Atomics](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/atomic/package-summary.html)
are also great – i do not have to think twice when implementing counters
or any other simple data structures.

most of the time i do not even have to work with threads or low-level
synchronization primitives directly – they are buried deep within the
libraries. i have less nightmares, since i do not have to touch
`volatile` as often.

at some point i’ve read both editions of [doug lea’s
book](http://www.amazon.com/Concurrent-Programming-Java-TM-Principles/dp/0201310090),
but i was always hesitant to recommend it; i’d rather rely on libraries
that abstracted all of this away. now that `java.util.concurrent` has
been out for 4 years, and [Java Concurrency in
Practice](http://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601)
has become a bestseller, there are no more excuses.

one thing i’ve learned though – when you think you got this stuff, you
discover a whole new class of problems that make you realize how
complicated all of this really is, and how truly difficult it is to
write larger concurrent programs.

you really, really have to think hard about how you share your objects,
how you compose them and operate on them. you need to really understand
how the language and the runtime work (i find myself checking [<span
class="caps">JLS</span>](http://java.sun.com/docs/books/jls/) quite
often). this is where good OO practices like encapsulation become even
more important, since you are not just risking maintenance overhead, but
you are risking the correctness of your program.

now, i always told myself that programming is not an exercise in
manliness. i am just an app developer; i want to ship a working code
that solves customer’s problems, not spend countless hours trying to
reason through non-blocking algorithms just because i decided to do
something non-trivial with
[ConcurrentHashMap](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/ConcurrentHashMap.html).
at the same time i do not want to waste my precious CPUs, so what am i
to do? shouldn’t this stuff be easier? is there something I am missing?

# threads considered harmful

<img src="/assets/2008/9/12/dijkstra.jpg" data-align="right" data-hspace="10" />

actually, there is no problem with threads per se; the problem is with
*shared state*.

in a normal sequential program you only worry about the logic as it is
unfolding before you – one statement after another, in order. in a
concurrent program that uses threads and shared state in addition to all
your usual problems you also have problem of the *non-deterministic
state*: since at any point in time any thread can come in and mess with
your data, even between the operations you considered atomic before
(like `counter++`), the number of states that your program can be in
suffers a combinatorial explosion. this makes it really hard to reason
about its correctness.

your code becomes brittle, sacrificing *failure isolation* – one
misbehaving thread can potentially harm the whole runtime (a good
analogy is [<span
class="caps">BSOD</span>](http://en.wikipedia.org/wiki/Blue_Screen_of_Death)
caused by a device driver).

in addition, things don’t *compose* – a transfer operation performed by
a thread-safe *customer* between two thread-safe *accounts* is not going
to be automatically thread-safe.

to make matter worse, some of the errors remain hidden when run on
commodity 1-2 <span class="caps">CPU IA32</span> hardware, but as the
number of CPUs grow, or their architecture becomes less restrictive to
help with concurrency, things start to break down.

for more thorough discussion see [The Problem With
Threads](http://www.eecs.berkeley.edu/Pubs/TechRpts/2006/EECS-2006-1.pdf)
by Edward A. Lee and Cliff Click’s [We Don’t Know How To
Program…](http://blogs.azulsystems.com/cliff/2008/04/we-dont-know-ho.html)

# now what?

a natural reaction is to forget about fine-grained parallelism and
offload the hard stuff onto someone else. after all, i am an app
programmer, i care about business problems, what’s all of this [yak
shaving](http://www.catb.org/jargon/html/Y/yak-shaving.html) about?!

in some cases we can get away with firing up individual processes to
take advantage of multiple CPUs. most of the time though it means that
the problem has been pushed further down the stack, which often turns
out to be the database. this is the route that
[rails](http://www.rubyonrails.org/) folks went, and it certainly was
pragmatic approach at the time (now that they are forced to deal with
efficiency, threading is back in the picture. for discussion of issues
see [Q/A: What Thread-safe Rails
Means](http://blog.headius.com/2008/08/qa-what-thread-safe-rails-means.html)).

if you can get away with using individual processes, go for it (see
[google chrome](http://www.google.com/googlebooks/chrome/small_04.html))
– you get *failure isolation*, you get *immutability* in respect to
other processes (it won’t be as easy for another process to mess with
your data), and as an additional benefit, you get to use all the
standard tools that the OS has when it comes to managing and
troubleshooting processes (as opposed to using often incomplete and
idiosyncratic tools for thread management that your runtime platform of
choice offers – if any).

still, as we need more and more fine-grained concurrency and as the
level of concurrency increases (it is not just a handful of CPUs now,
but dozens, and even [hundreds](http://www.azulsystems.com/)), one
process per task becomes too expensive (context switching, high costs of
creating a new process, memory overhead, etc). so we are back to some
sort of lightweight thread-like primitives running within the same
process, sharing some common resources.

most of the popular languages/platforms these days provide some sort of
threading and shared memory support. but as outlined above, they suffer
from some fundamental problems. there are some practical things at
various levels of abstractions that that can help: low-level constructs
within the language/platform itself, tooling, and higher-level
libraries/[mini-languages](http://en.wikipedia.org/wiki/Domain_Specific_Language)

#### language

-   make *immutability* easier – take note of functional languages, but
    also make it practical. in java case, for instance, it could mean
    extending immutability to some core data structures (see
    [scala](http://www.scala-lang.org/) collections) or making it easier
    to tag an instance as immutable
    ([see](http://www.ruby-doc.org/core/classes/Object.html#M000354)
    ruby’s `freeze`; this reeks of boilerplate though) – this way errors
    will be caught at compile time
-   consider sharing data only through explicit, ideally checked at
    compile-time, means. thus by default nothing is shared, and in order
    to make something shared you have to explicitly tag it as such.
    ideally, this would also come with some sort of namespace support,
    thus limiting mutations to a sandbox (see
    [clojure](http://clojure.org/concurrent_programming) for reference)
-   make language safer to use when it comes to exposing shareable state
    (this is when something like `static` [becomes a
    problem](http://gbracha.blogspot.com/2008/02/cutting-out-static.html)
    – see [Shared Data Considered
    Harmful](http://blog.headius.com/2008/04/shared-data-considered-harmful.html)
    for an example that applies to concurrency)

#### tooling

-   static analysis tools might help, but we need to give them a bit
    more than just an infinite number of states.
    [findbugs](http://findbugs.sourceforge.net/) for instance, supports
    [concurrency
    annotations](http://www.javaconcurrencyinpractice.com/annotations/doc/index.html)
    and something like [chord](http://chord.stanford.edu/) could also be
    promising. this stuff is complex though and there are limits to
    static analysis (and i do not even want to bring up formal proofs
    using [process
    calculi](http://en.wikipedia.org/wiki/Process_algebra))
-   i want more support from the platform to help me troubleshoot lock
    contention, deadlocks, cpu-intensive threads, and other
    concurrency-related infrastructure. sun’s hotspot has some
    [rudimentary](http://java.sun.com/javase/6/docs/technotes/guides/visualvm/index.html)
    [stuff](http://java.sun.com/javase/6/docs/technotes/guides/management/jconsole.html)
    in place, but i want more things out of the box
    ([azul](http://www.azulsystems.com/) claims that they have always-on
    built-in tools in their product, but i have not played with them)
-   speaking of azul, i need to study them more. although perceived as a
    boutique solution, they are addressing issues that everyone will be
    facing in just a few years. seems like they ported sun’s hotspot to
    their hardware which allowed them to achieve scaling by
    automatically replacing synchronization with [optimistic
    concurrency](http://en.wikipedia.org/wiki/Optimistic_locking) which
    scales much better. incidentally, this truism about optimistic
    concurrency has been obvious to database folks for decades

#### libraries/mini-languages

one of the approaches is to focus on your problem domain and come up
with a library/language that solves your particular problem and
abstracts away concurrency. web frameworks (J2EE, rails), or <span
class="caps">ETL</span> tools, or even databases are all examples of
such approaches.

this is where my interest lies as an app developer – how can i make
concurrent programming easier for me, the layman.

the bottom line is that if we insist on using low-level synchronization
primitives, it would be really hard to paper over the underlying
complexities. right now there is no generic universal approach that will
simplify concurrent programming. so at this point a pragmatic programmer
is left with patterns, supporting libraries, and heuristics.

# to be continued

there are some patterns (for the lack of a better word) that i found to
be helpful in dealing with concurrency; there is also some stuff on the
horizon that promises all sorts of benefits – is there really a silver
bullet? but also there is plenty of stuff that has been with us for
decades, and i would be the first one to bow my head in shame,
acknowledging my ignorance.

-   [part 2](/2008/9/19/concurrency-part-2-actors)
