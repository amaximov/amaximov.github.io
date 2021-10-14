---
permalink: /2005/11/14/e-tag-and-server-farms
date: '2005-11-14 16:44:00'
title: >-
    e-tag and server farms
---

most of the people do not do much with e-tag http response headers, and
it's probably ok, unless one is really trying to get the most out of
client-side caching.

[this](http://studio.tellme.com/vxml2/ovw/perf/cache_apache13.html) has
been written for apache 1.3.x, but is still relevant for apache 2.x:

> An ETag is an HTTP response header returned by an HTTP /1.1 compliant
> Web server such as Apache 1.3x. By default, Apache calculates an ETag
> for a requested file using a combination of the file's location in the
> file system (I-Node number on Unix systems), its modification time,
> and its size. \[..\]
>
> Because the ETag is calculated using the file's I-Node, and an I-Node
> is machine-specific, administrators of Web server farms will
> experience unexpected requests if the ETag differs from machine to
> machine.
>
> To work around this issue, use the FileETag directive to configure
> your Apache server to use only the file modification time and file
> size when calculating the ETag.
>
> The following example configures Apache to only use the modification
> time (MTime) and size (Size) when calculating the ETag for any file
> contained in the /usr/local/httpd/htdocs directory or a subdirectory.

    <Directory /usr/local/httpd/htdocs>
    FileETag MTime Size
    </Directory>

in other words, if you are running multiple web servers that serve
static content for which apache provides e-tag response headers, it
might make sense to use the directive above to make sure that e-tag
header values are not different from machine to machine for the same
content. i confirm that this is the case in unix, but i have not
verified this on windows.
