---
permalink: /2007/9/27/for-fun-and-profit
date: '2007-09-27 22:38:00'
title: >-
    for fun and profit
---

if you enjoyed everyone’s favorite
[upside-down-ternet](http://www.ex-parrot.com/~pete/upside-down-ternet.html)
way of [making new
friends](http://en.wikipedia.org/wiki/How_to_Win_Friends_and_Influence_People),
this whimsical bit is right up your alley.

it is based on [cross-site request
forgery](http://shiflett.org/articles/cross-site-request-forgeries)
(CSRF) attack.

briefly, these are the attacks that trick you into submitting a
potentially damaging request to the application you are logged in to. so
if you receive an email with a link to
`http://www.google.com/setprefs?hl=ga`, which you press, it will set
your google language preferences to irish.

thus you could try to impress those inquisitive souls looking for things
on your site with the following apache config directive:

    RedirectMatch \.(php|phtml|phps|php3)$ http://www.google.com/setprefs?hl=xx-klingon

therefore any request to a booby-trapped url on your site (in this case
anything that ends in php) would set their google search language to
klingon.

<img src="/assets/2007/9/28/laughter.jpg" data-align="right" data-hspace="10" />

(stolen from [here](http://isc.sans.org/diary.html?storyid=1750))

of course, it does not have to be an explicit server-side redirect –
similar behavior can be triggered with javascript, iframes, etc.

how do you protect from it? the app has to use unique tokens in the form
presented to the user (or one can start lugging around those encrypted
URLs again – anyone remembers IBM’s
Net.Commerce?)

since i am (somewhat reluctantly and half-asleep) reading [gibson’s
latest](http://en.wikipedia.org/wiki/Spook_Country), and since these
days i mostly appreciate him for sensing the zeitgeist and popularizing
new art forms, i cannot shake off the feeling that there is an art piece
lurking in here.
