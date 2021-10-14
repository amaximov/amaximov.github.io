---
permalink: /2006/7/4/hall-of-shame
date: '2006-07-04 21:05:00'
title: >-
    hall of shame
---

how do you know that an IT department has failed? when the users, after
repeated requests to help them out with building a small custom content
management system, turn around, get a server at ev1 servers, and build
their app there.

now just stop and think about that for a second. this is just insane! i
felt ashamed (of my department, my profession, my title) when i heard
about it (especially since my title does have the words "architect" and
"enterprise" in it). business users wielding developer tools, trying to
replace email chains with spreadsheet attachments, and an IT department
that is so bent on "enterprise" and "no more custom development, all
packaged products!", that it fails to see a direct immediate need that
could be easily filled with just a few weeks of quick hacking in
something like coldfusion (or even java, or less "enterprise-y"
php/rails for that matter).

granted, if each department goes off and builds their own silos with
custom apps, this would be a disaster (ms access app that lives on a
shared drive), and the other extreme is true - packages for everything,
no more custom development; all or nothing - big bang enterprise
solution or email and spreadsheets.

now without knowing all the details, the ideal scenario would have been
for the enterprise integration architecture dudes to built a universal
standard layer to access enterprise data, and then let the departmental
teams go nuts with their own stuff, as long as they conform to a loose
set of guidelines on architecture for their apps - supported platforms,
some development standards, hands-on enterprise architect on a project,
etc. a lot of this department-level stuff should be developed in rapid
prototyping language - something scripting, something that is
web-enabled, and something that can get things solved fast. the danger
is a quick sprawl of spaghetti, and this is where good internal dev
teams are important - mentoring, common code ownership, etc. i have seen
over and over again how quick rapid app thrown in gets the biggest bang
for the effort spent, so we just need to make sure we get the core
backend right, and then build systems smarter.

in the interim, perhaps they could have looked at a wiki like
confluence, or even at sharepoint+infopath combo that is sadly grossly
misused and abused here, but has so much potential, no matter how much i
hate standalone sharepoint (probably for all the wasted potential).

we used a lot of cold fusion back in the day, and now the swing is into
the Java world and people stopped developing the apps as much as they
used to, because the barrier for entry is so high with java. some of it
was the backlash against poor developers writing unmanageable apps in
cold fusion, but the benefit was an ability to build things fast to help
the users. we need to bring this back, but be smarter about integration
points with enterprise data. those should be architected/engineered
properly, but smaller departmental apps should be built on top of them
using glue languages and lighter technologies that lend themselves well
to continuous evolution (because, as we know it, the application is
never "done"; it is finished only when users stop using it).

i think this is why i am so sensitive to the "architecture astronaut"
syndrome; we need to be able to see the big picture, but focus on the
end users, "empower" and "enlighten" the developer "masses" that are
closer to the business, help them build faster, smarter apps that get
the work done. i know i lack a lot of knowledge in the custom app space
for this industry, and a lot of the problems are already solved by these
large packages, but there will always be the need for something smaller,
quicker, more agile built on top of these large enterprise apps that
would greatly benefit small groups of users.
