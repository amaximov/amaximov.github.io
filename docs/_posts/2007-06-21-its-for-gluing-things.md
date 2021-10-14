---
permalink: /2007/6/21/its-for-gluing-things
date: '2007-06-21 14:31:00'
title: >-
    it's for gluing things
---

i have installed [xml-rpc
plugin](http://www.trac-hacks.org/wiki/XmlRpcPlugin "xml-rpc plugin")
for [trac](http://trac.edgewall.org/ "trac") and played a bit with it.
it is amazing how simple it is to use - just install the plugin, add a
user to the basic auth passwd file (in my case Apache checks there
first, then goes to Active Directory), give this user XML_RPC privilege
in trac admin, and there you go:


    #!python
    import xmlrpclib
    server = xmlrpclib.ServerProxy("http://username:password@host/trac/login/xmlrpc")
    print server.wiki.getPage("WikiStart")

just imagine the possibilities that make trac an application platform -
easily create pages/attachments or edit entries in response to events
(we have scripts that do certain things for us, and then we also have to
go into the wiki and document things manually), create pages in response
to incident tickets as they are being worked on, or functional
specification workflow process, etc, etc.

xmlrpc libraries are built into python and ruby (php and even
javascript, not to mention java) - so there is nothing really that stops
one from running this thing on a stock installation of a given language
(non-privileged account on a unix box, for instance).

here's a simple script i put together to backup a snapshot of trac wiki
to a local hard drive; it is using ruby, since my python skills are nil
(i do like the python xmlrpc api much more though - it seems to be a lot
more convenient to use and succinct, compared to
[xmlrpc4r](http://www.ntecs.de/projects/xmlrpc4r/client.html "xmlrpc4r")):

``` ruby
#!ruby
require 'xmlrpc/client'
require 'fileutils'

class Wiki
  def initialize
    @client = XMLRPC::Client.new2('https://user:password@server/trac/login/xmlrpc')
  end

  def method_missing(m, *args)
    @client.call('wiki.' << m.to_s, *args)
  end
end

wiki = Wiki.new
pages = wiki.getAllPages

index = '<html><body><ul>'

pages.sort.each do |p|
  puts 'getting ' << p
  FileUtils.mkpath p

  txt = wiki.getPage p
  html = wiki.getPageHTML p

  open(File.join(p, 'index.txt'), 'w') { |f| f.puts txt }
  open(File.join(p, 'index.html'), 'w') { |f| f.puts html }

  attachments = wiki.listAttachments p
  attachments.each do |a|
    puts "\\t" << 'getting attachment ' << a
    content = wiki.getAttachment a
    open(a, 'wb') { |f| f << content }
  end

  index << '<li>' << p << '<ul>'
  index << '<li><a href="' << p << '/index.html">html</a></li>'
  index << '<li><a href="' << p << '/index.txt">txt</a></li>'

  if !attachments.empty?
    index << '<li>attachments</li>'
    index << '<ul>'
  end

  attachments.each do |a|
    file = File.basename a
    index << '<li><a href="' << p << '/' << file << '">' << file << '</a></li>'
  end

  index << '</ul>' if !attachments.empty?

  index << '</ul></li>'
end

index << '</ul></body></html>'

open('index.html', 'w') { |f| f.puts index }
```

i am not using multicall, since it only takes a few minutes to run
against our trac instance.

more information on the wiki xml-rpc interface is
[here](http://www.jspwiki.org/Wiki.jsp?page=WikiRPCInterface2 "wiki xml-rpc interface").
seems like trac does not implement listLinks as well as listBackLinks
and some macros do not render properly when retrieving pages via
getPageHTML.

also, since
[tags](http://www.trac-hacks.org/wiki/TagsPlugin "trac tags plugin")
(which we use heavily) are an extension to trac, xml-rpc api does not
support them. perhaps a weekend project to add that in?
