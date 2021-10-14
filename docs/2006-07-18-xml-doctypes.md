---
permalink: /2006/7/18/xml-doctypes
date: '2006-07-18 20:25:00'
title: >-
    xml doctypes
---

something that bit me recently: editing `sqlmap-config.xml` for ibatis
and getting strange xml validation errors during deployment:

    Error parsing XML. org.xml.sax.SAXParseException: Element type "sqlMapConfig" must be declared.

the file looked perfectly fine and myeclipse happily validated it (i
could change a property and get a validation error), however, during
deployment it failed

it turns out that the problem was in the DOCTYPE declaration. what i had
was

    <!DOCTYPE sqlMapConfig
      PUBLIC "-//ibatis.apache.org//DTD SQL Map 2.0//EN"
      "http://ibatis.apache.org/dtd/sql-map-config-2.dtd">

what i should have had was

    <!DOCTYPE sqlMapConfig
      PUBLIC "-//ibatis.apache.org//DTD SQL Map Config 2.0//EN"
      "http://ibatis.apache.org/dtd/sql-map-config-2.dtd">

a small typo that cost me a couple of hours of grief and confusion.
reading up on it
[here](http://www.freebsd.org/doc/en_US.ISO8859-1/books/fdp-primer/sgml-primer-doctype-declaration.html),
i learned that what threw me off was a Formal Public Identifier (FPI)
that has the following syntax

    "Owner//Keyword Description//Language"

therefore my `description` was incorrect. once it was fixed, everything
worked as expected.

i suppose i knew that browsers, for instance, use the doctype
description to figure out which parser to use, but i guess in this case
i expected a gentle warning message in the console, a soft friendly
whisper from the IDE - not globs of violent stacktraces.
