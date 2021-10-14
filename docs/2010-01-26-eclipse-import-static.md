---
permalink: /2010/1/26/eclipse-import-static
date: '2010-01-26 17:19:00'
title: >-
    eclipse import static
---

i very much believe in a [craftsman approach to software
development](http://en.wikipedia.org/wiki/Software_Craftsmanship),
which, among other things, advocates the value of mastering the tools in
your toolbox.

i consider using keyboard shortcuts in your <span
class="caps">IDE</span> of choice a part of this craftsmanship approach.
i do sympathize with [unclebob’s
plight](http://blog.objectmentor.com/articles/2009/11/21/whats-all-this-nonsense-about-katas)
for mouse-less editing and with [stevey’s earlier posts on the
subject](http://steve-yegge.blogspot.com/2008/09/programmings-dirtiest-little-secret.html).

back in 2004 java5 went GA and introduced [static
imports](http://java.sun.com/j2se/1.5.0/docs/guide/language/static-import.html)
among several other syntactic niceties.

this feature is most useful for static helper methods – instead of
writing `Assert.assertEquals`, i would rather use `assertEquals`, since
i know i am writing a test, and in the domain of testing, `assertEquals`
does not need to be qualified. same goes for many internal utility
methods that i tend to use a lot (e.g. `asList()`) or static factory
methods (e.g. `newDateTime()`). as a side note, using `newXY()` as a
static factory method as opposed to `create()` makes it more suitable
for static importing.

in my current <span class="caps">IDE</span> (Eclipse) i rely on
~~auto-completion~~ Ctrl+1 programming, so i would start typing
`Assert.`, followed by `Ctrl+Space` and then manually convert normal
`import` to `import static`. it was *very* undignified.

it turns out that in Eclipse `Ctrl+Shift+M` that i already used to
import dependencies under the cursor, also works for converting static
method calls into static imports.

now all i have to do is type `Assert.assertEquals` once, then press
`Ctrl+Shift+M` (obsessively followed by `Ctrl+Shift+O` to organize
imports), and i can start using `assertEquals` all over the place
without qualifying it with `Assert`.

as an additional convenience, i always set *Number of static imports
needed for .\** to 1 under *Java -> Code Style -> Organize Imports* in
Eclipse preferences. this way a single static import of a method from
`Assert` triggers import static of `Assert.*`, which is what i want.
