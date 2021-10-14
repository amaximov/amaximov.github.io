---
permalink: /2006/12/17/why-wiki-continued
date: '2006-12-17 21:47:00'
title: >-
    why wiki, continued
---

[our team has been running on trac for past four
months](http://blog.splitbody.com/articles/2006/09/04/why-wiki "why wiki"),
and the results so far were very encouraging. we organize things under
coarse-grained categories, and then use
[tags](http://www.trac-hacks.org/wiki/TagsPlugin "trac tags") to
organize content further. tags really help out a lot, i got so used to
CLI-like searching (`/trac/tags/tag1+tag2`), and their indexing
capability (`ListTagged()` macro).

a few things learned:

<img src="/assets/2007/8/27/workers_formula.jpg" data-align="right" data-hspace="10" />

-   wikis work best for small homogeneous groups, and even then only a
    few "expert" people contribute; sadly it is not the whole group that
    enthusiastically uses the wiki as a group's collective knowledge
    base, as well as communication device (perhaps it is a nature of our
    environment though)
-   it works really well as a metadata "glue", when it pulls together
    different sources in one context (a few links to documents in
    sharepoint, a few links to some internal systems, and some text to
    describe it all). i would really like to extend this further and
    start consuming stuff from other apps (syndicate feeds, pull in
    reports, etc. for instance - every morning create an entry for past
    night's batch run issues from the report we currently have, so that
    person on call can start annotating it as issues are worked on)
-   i really need an auto-save feature (gmail and the like). since i am
    trigger-happy on the keyboard, i've lost posts a number of times. it
    should be trivial to implement. on a side note, i thought i would
    hate the new spelling support in firefox, but i find it incredibly
    beneficial
-   tags are great, but the consistency of tag corpus is an issue;
    self-imposed rules help a bit (nouns, no plurals, lowercase, etc),
    but a del.icio.us-like drop-down of suggestions as you type would be
    very helpful
-   i haven't really needed to search through attachments yet using
    trac, but then we still store most of our binary docs in sharepoint.
    the funny thing is that people save bigass ms office documents in
    sharepoint with revision tracking turned on (40M documents are not
    uncommon), which forced sharepoint admins to turn off versioning
    across the board, defeating one of the main benefits of sharepoint
    (apparently our version did not use binary diffs, saving full
    content every time). on top of that search within documents in our
    version of sharepoint is pretty much useless anyway. so considering
    all this i am thinking of just asking people to map a branch of our
    svn repo as a drive and save documents there; although it might
    result in a lot of commits, it would be versioned and in addition
    mapped into our website's namespace
-   need for templates - as we start to store more structured content
    like technical specifications or high-level interface descriptions
    that have certain required fields
-   and the final wish, or more of a pipedream - smarter markup that has
    semantic value that could be harvested/searched/aggregated
    (something along the lines of a yet-to-be-realized promise of
    xml-based backend of ms office) with support for intellisense-like
    autocompletion. as mentioned above, as we start storing interface
    descriptions that have certain common fields (source system, target
    system, integration technology, group that owns it, canonical data
    format used, etc), i want to be able to run queries like "show me
    all interfaces owned by this group", or "show me all interfaces that
    use this integration technology", or "show me all interfaces that
    feed this system". then i want to save these queries and make them
    dynamic, so essentially they become different views into the data.
    sharepoint currently supports it with excel-like functionality and
    views, but the content is strictly tabular. what i want is the
    ability to use one of these domain-specific markup
    [microformats](http://en.wikipedia.org/wiki/Microformat "microformats")
    as i am writing my wiki entry. i can hackily mimic this to an extent
    with "typed" tags (i.e. `interface/source/systema`,
    `interface/technology/toolb`), but it just feels way too flimsy.
    [jon udell's continuous laments on this
    subject](http://del.icio.us/judell/informationarchitecture "udell on infoarch")
    were very inspiring.
