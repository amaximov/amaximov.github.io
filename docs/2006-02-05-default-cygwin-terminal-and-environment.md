---
permalink: /2006/2/5/default-cygwin-terminal-and-environment
date: '2006-02-05 13:17:00'
title: >-
    default cygwin terminal and environment
---

anyone that installed cygwin and used it out of the box knows about the
limitations of the default terminal: those awkward scrolling errors,
resizing pain, limits on the scroll buffer, colors, etc.

i never bothered to get it fixed. until now that is. use `rxvt` instead
(you need to install it first): create a shortcut with the following
command line:

    D:\\programs\\cygwin\\bin\\rxvt.exe \\
    -vb -sr -sl 20000 \\
    -fn courier \\
    -g 120x50 \\
    -e /usr/bin/bash \\
    --login -i

`man rxvt` to see what those actually mean. then edit your
`.bash_profile` (in case your $HOME is unnatural and your `.bashrc` does
not get read) and add the following:

    alias less='/bin/less -r'
    alias ls='/bin/ls -F --color=tty --show-control-chars'

you should also put the following in your `.vimrc`:

    syntax enable
    filetype on
    filetype plugin on
    set ts=2
    set number
    set ai
    set si

and you also might want to grab [rhtml syntax plugin for
vim](http://www.vim.org/scripts/script.php?script_id=403).

this will get the expected stuff working (ctrl-pgup/pgdn, colors, proper
terminal handling when you login to remote hosts via ssh, etc). note
that you copy on selection and paste with the middle mouse button or
`shift-insert`.
