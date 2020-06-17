---
title: "Quick start Tmux"
date: 2020-06-17T10:00:00
categories:
  - blog
tags:
  - tmux
  - terminal
  - rough cuts
---

Quick start Tmux

Run up a bash terminal then:
```bash
$ tmux
```

Note this is a key sequence, not all keys pressed at once.
```
ctrl-b, %	split the screen in half from left to right
ctrl-b, "	split the screen in half from top to bottom
ctrl-b, x	kill the current pane
ctrl-b, <arrow key>	switch to the pane in whichever direction you press
ctrl-b, d	detach from tmux, leaving everything running in the background
$ tmux attach, reattach
```

It is highly recommend to remap the main binding from Ctrl-b to something like Ctrl-c or Ctrl-a

```bash
$ vi ~/.tmux.conf
```
Setting to Ctrl-a, nice if you used `Screen` before.
```
set -g prefix C-a
```

Reference
https://blog.hawkhost.com/2010/06/28/tmux-the-terminal-multiplexer/

