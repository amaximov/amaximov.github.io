---
permalink: /2010/2/1/qcon2009sf-individual-talks
date: '2010-02-01 05:57:00'
title: >-
    qcon2009sf: individual talks
---

[as promised](/2009/12/4/qcon2009sf), these are a few talks that i have
attended and found worth mentioning. i know i missed a lot due to
scheduling conflicts, but that’s the nature of the game.

## [clojure talk by stu halloway](http://qconsf.com/sf2009/presentation/Clojure+in+the+Field)

a great talk that had to be witnessed; it was a fast-paced flight
through the language, illuminating its features and defining its place.
there was a story, there was excitement, and there was a pragmatic take
on it all. since languages track was aimed at actual usage in the field,
half of the talk was spent on war stories – things that worked and
things that did not. it was a tight, erudite talk, with just the right
amount of details.

i am still ambivalent about the language – i do not have enough
experience with it to see it used in production on the systems i am
working on right now; it still exhibits growing pains, and feels a
little rough around the edges. perhaps it is my lack of functional
language exposure that shows. at the same time i am absolutely
fascinated and excited about the things that it gets right – the
immutable data structures and the whole concurrency story. the language
feels nimble, finely honed, and it is great to witness its evolution, as
it happens in front of my eyes. i love the way it makes my brain feel,
the way it challenges my perspective on language design and features.

if tech is your competitive advantage, and you have small sharp teams,
then by all means, give it a try. even if the language does not survive
in its current state, the ideas and their implementation will live on –
i think they are that important.

## [groovy on the trading desk by jonathan felch](http://qconsf.com/sf2009/presentation/Groovy+on+the+Trading+Desk)

there is always a bit of a stigma associated in my mind with conference
“thought leaders” – unless they have proven their credibility by
repeatedly building and shipping, i always take their words with a grain
of salt. after all, those that have the time to float from conference to
conference, from client to client, might (d)evolve into pundits. there
is a definite value in that, and i certainly would still attend their
talks and buy their books, but i would always remind myself of their
perspective.

i really liked jonathan’s talk because it was ruthlessly pragmatic,
coming from someone driven to ship, working with traders to solve real
problems quick. in a sense, this environment is somewhat of an
aberration, since outside of the trading desk the software development
world is quite different.

his team was bending technology, doing very creative things right on the
bleeding edge; by any means necessary they had to deliver software for
the business under the tightest deadlines. in some respects, this is the
technologist’s ultimate dream – when politics and money and all the
other pressures of architecture and enterprise world are pushed aside
and all that matters is whether you can deliver. this freedom is scary
and exciting at the same time.

the talk was about a distributed computational in-memory engine they
have built to support a trading desk, standardizing on groovy and
building on top of terracota in 2006. this allowed them to deliver new
features in a matter of hours for their traders.

essentially it was a graph where cascading properties were recomputed in
response to events; logic could be injected via closures at runtime,
state and behavior of individual nodes could be extended at runtime; all
of it written in functional style, avoiding shared state.

he talked about the areas where groovy shined, and walked through some
of the problems they have run into. predictably, the strength was
writing DSLs, terseness, convenience, speed of writing code, dynamic
nature, integration with other systems; pains were performance, math,
and language gotchas.

jonathan also managed to give a perspective on quantitative finance in
general – what is the business about, who are the people involved, what
tech is used, and what problems they have to deal with. this is what
really made the talk “sink in.”

i dismissed groovy early on, when the race to add new language features
trumped the need for quality and thoroughness. the whole affair seemed
to be too sloppy and haphazard, so i only watched its evolution from the
distance. i suspect that the situation has changed, even before spring
source acquisition, so i should give groovy another try.

## [architecture for the cloud by michael nygard](http://qconsf.com/sf2009/presentation/Software+Architecture+for+Cloud+Applications)

i am yet to read ["release
it"](http://pragprog.com/titles/mnee/release-it), but i have come to
appreciate his perspective based on the articles, blog entries, and book
excerpts. i think michael has a great gift for organizing and presenting
the patterns of operations architecture, a field that for the longest
time has been the dirty secret of running systems; the proverbial “last
mile” of software development, the achilles’ heel.

it takes someone straddling the fence between operations and developers
to recognize the issues. having been in this role myself (and having
ranted about it on this very blog), i am really grateful to him for
illuminating and organizing the patterns in a manner that (hopefully)
should help us as a community to avoid repeating the same mistakes.

why do patterns matter? it is a shared language that allows those
responsible for operations and development to communicate with each
other and recognize the problems and their solutions.

why does operations matter even more now? the proverbial admin/developer
fence is disappearing, cloud means fast provisioning of many machines
done by developers/users; the developers become more and more aware of
infrastructure, which, in turn, becomes more of a commodity, while the
job of the sysadmin is changing. i really liked his practical insights
into the way cloud computing will be changing the roles within the
enterprise.

overall, i mostly nodded along with the slides, but it helped me
organize my own thoughts on the subject (which, in the end, might be far
more important).

## [doug crockford on javascript](http://qconsf.com/sf2009/presentation/The+State+and+future+of+JavaScript)

an immensely entertaining and sprawling talk that went into the history
of the language, its evolution, and its future. it was exactly the kind
of the talk i [dismissed earlier](/2009/12/4/qcon2009sf), but at the end
of the long day, and from someone as entertaining as doug turned out to
be, i was ready to kick back and enjoy the ride. there were plenty of
anecdotes and killer one-liners, so if you get a chance, watch him
speak.

## [erik meijer on rx](http://qconsf.com/sf2009/presentation/Democratizing+The+Cloud+With+The+.NET+Reactive+Framework+Rx)

as opposed to the doug’s talk mentioned above, this was a great example
of a conversation, or *riffing*, where ola bini, don box, dan north,
amanda laucher, sadek drobi, and a few others completely derailed the
whole rx presentation into a joyous bantering about languages.

erik meijer is a joy to listen to as it is, but if you add a small
responsive audience and a few beers, the whole experience is
unforgettable. he loves to be paradoxical, and he revels in controversy.
he was dropping tweetable gems at an astonishing rate – the sparks were
flying, and my brain could hardly handle it.

at last we were pretty much forced out of the room by the staff – it was
a perfect closing for the conference.
