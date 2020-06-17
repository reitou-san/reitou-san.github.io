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

