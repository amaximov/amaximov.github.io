---
permalink: /2008/2/1/junit-joys
date: '2008-02-01 00:52:00'
title: >-
    JUnit Joys
---

i have been wrestling with some legacy code recently. beating it over
the head with a copy of [Working Effectively with Legacy
Code](http://www.amazon.com/Working-Effectively-Legacy-Robert-Martin/dp/0131177052/)
did not do much, so i started writing tests to see how it worked.

<img src="/assets/2008/2/1/working_effectively_with_legacy_code.jpg" data-align="right" />

after a few minutes of waiting for eclipse +
junit4.3.1[^1] combo to load, i furiously coded a bunch
of tests, and then realized that i could not make them fail. essentially
it boiled down to the following:

``` javascript
assertEquals(1.0, 1.1);
```

...which quietly and happily passes. wtf?!! these are two doubles, just
compare them and let’s move on with our lives!

then after a bit of thinking i recalled that most of my tests that
involved doubles were written on projects that were still on jdk \< 1.5,
when method above simply won’t even compile, alerting me to the fact
that junit expects [assertEquals(double, double,
delta)](http://junit.sourceforge.net/javadoc/junit/framework/Assert.html#assertEquals%28double,%20double,%20double%29),
where delta is the precision you need.

why they couldn’t simplify my life by creating a couple of `Double`
instances and calling `equals()` on them is beyond me. this is what i
would want most of the time anyway.

since i was running tests under jdk1.5, autoboxing kicked in and now we
have two `Double`s on our hands. fine, this should not be a big deal,
simply call `double1.equals(double2)` and be done with it – what’s a big
deal?

but nooooooooo, check out [this little bundle of
joy](http://junit.cvs.sourceforge.net/junit/junit/src/org/junit/Assert.java?view=markup&pathrev=r43):

``` javascript
private static boolean isEquals(Object expected, Object actual) {
    if (expected instanceof Number && actual instanceof Number)
        return ((Number) expected).longValue() == ((Number) actual).longValue();
    return expected.equals(actual);
}
```

what the hell?!! you correctly detect that this instance of `Double` is
an instance of `Numeric`, then take its long value and throw fractional
part out. quietly. so all my tests never even squeak. why?!!!

an obvious approach is to suck it up and appease the api:

``` java
assertEquals(1.0, 1.1, 0);
```

this will work. but damn! my eyes!!

# TestNG

we all know that junit is legacy, and version 4 was an afterthought, so
let’s see what [testng](http://testng.org/) does. [the
api](https://testng.dev.java.net/source/browse/testng/src/main/org/testng/Assert.java?view=markup)
is the same, and under jdk1.5 my primitives get autoboxed into `Double`s
and `assertEquals(Object, Object)` gets called:

``` javascript
public static void assertEquals(Object actual, Object expected, String message) {
    if (expected == null && actual == null)
        return;
    if (expected != null && expected.equals(actual)) {
        return;
    } else {
        failNotEquals(actual, expected, message);
        return;
    }
}
```

voila! this is exactly what i expected. and guess what – it actually
works and correctly fails the original test.

<img src="/assets/2008/2/1/testng.jpg" data-align="right" />

# Lessons

-   man, this alone would scare me away from junit in favor of testng
-   make sure your test fails before it ever works!
-   what really frightens me is how many more of these quiet autoboxing
    errors are lurking out there. what previously would be caught by the
    compiler now silently works in unpredictable ways
-   yet another thing to be aware of when upgrading your app from
    jdk1.\[34\] to jdk1.5+

# Note

this junit bug has been fixed in
[junit4.4](http://junit.cvs.sourceforge.net/junit/junit/src/org/junit/Assert.java?revision=1.7&view=markup&pathrev=r44)
and up

# Ruby

interestingly enough, on a few skunk works projects this year i cobbled
together a bunch of existing libraries with ruby glue and used (j)ruby’s
[Test::Unit](http://www.ruby-doc.org/stdlib/libdoc/test/unit/rdoc/classes/Test/Unit.html)
(which conveniently comes with ruby distro) and
[rspec](http://rspec.info/) for testing the result.

it definitely makes sense for a project that is written in (j)ruby that
uses many existing java libraries; it might be a bit of a mindset shift
for a java project that is looking for simplified testing. for now i am
keeping an eye on projects like [JtestR](http://jtestr.codehaus.org/)

[^1]: default version of junit that ships with eclipse 3.3
