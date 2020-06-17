---
title: "Bash Terminal Ninja"
date: 2020-06-11T10:00:00
categories:
  - blog
tags:
  - bash
  - rough cuts
---

This is a big work in progress. I discovered a "few" useful bash tricks but when I started researching further I found a huge number of manuals and discussions. All I wanted was a quick way to fix mistakes in a really long command without trawling one character at a time using arrow keys.


Moving forward/backwork through your command one word at a time (whitespace delimited).
```
ALT-F -> move forward one word
ALT-B -> move backward one word
ALT-D -> delete word under cursor or next word if on white space
CTRL-C -> undo these commands
CTRL-A -> move to start of line
CTRL-E -> move to end of line
```


`!$` the `end` of the previous command
```bash
$ grep findthingthing thelisttosearch.txt
$ vi !$

<vim opens 'thelisttosearch.txt'>
```




Automatic breakdown of command line arguments:
https://www.explainshell.com/


Links/Manuals

https://tiswww.case.edu/php/chet/bash/bashref.html

https://courses.cs.washington.edu/courses/cse390a/14au/bash.html

https://web.archive.org/web/20130901181242/http://deadman.org/bash.php

https://www.howtogeek.com/howto/ubuntu/keyboard-shortcuts-for-bash-command-shell-for-ubuntu-debian-suse-redhat-linux-etc/

https://opensource.com/article/20/6/bash-history-commands

