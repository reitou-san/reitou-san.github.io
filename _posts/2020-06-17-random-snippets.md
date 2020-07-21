---
title: "Random Snippets"
date: 2020-06-17T10:00:00
categories:
  - blog
tags:
  - random
  - rough cuts
---

Command line zlib decompression + header
```bash
$ printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" | cat - yourfile.text | gzip -dc > temp
```

```bash
# grab the first 18 chars from a string
echo 'your giant string here' | head -c 18 | wc -c
# or
echo 'your giant string here' | dd bs=1 count=18 | wc -c
```