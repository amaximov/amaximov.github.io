---
permalink: /2006/3/18/rails-native-mysql-bindings-and-different-mysql-versions
date: '2006-03-18 01:09:00'
title: >-
    rails, native mysql bindings, and different mysql versions
---

a simple setup: i have a system-wide mysql 4.0 install. i have some
rails apps running under that. i have another few apps that need mysql
5.0.

that should be simple, right? install mysql 5.0 into its own isolated
directory, point the app's driver/adapter to that database and we are
done (at least this is the java way).

except in ruby the native bindings are installed in the core of the
language itself (even if they were not, with the separate gem's home
setup, as they should be), so i have to recompile them in a
not-so-obvious manner, passing them the config parameter (not documented
in the gem manual):

    gem install mysql -- --with-mysql-dir=/usr/local/mysql5/current

so ideally i should be able to have my own adapter on per-application
basis. i guess this is a drawback of relying on the native bindings
(java does not, for example).
