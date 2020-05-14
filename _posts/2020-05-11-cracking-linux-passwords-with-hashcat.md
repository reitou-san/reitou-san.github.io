---
title: "Cracking Linux Passwords With Hashcat"
date: 2020-05-11T09:12:34
categories:
  - blog
tags:
  - hashcat
  - cracking
  - passwords
---

First of all, breaking user passwords in Linux requires access to the `/etc/shadow` file.

The usual scenario is that access to the target machine has had a privilage escalation to root. Privilage escalation is a subject in itself and will not be covered here.

So for this example we will just be using a 2020 Kali linux machine with access to the `/etc/shadow` file.

On Kali linux the default login configuration is located in `/etc/login.defs` and the hashes, as already mentioned, at `/etc/shadow`

`/etc/login.defs` defines `ENCRYPT_METHOD` with the default value `SHA512` Encryption rounds can also be set in this file but by default are not and therefore allows the default value to take which is 5000 rounds. The comments under `ENCRYPT_METHOD` give all the details.

```
$ sudo grep ENCRYPT_METHOD /etc/login.defs
ENCRYPT_METHOD SHA512
```

The hash type can be different and should be verified so that the correct type is set for hashcat.

```
SHA-512 $6$
SHA-256 $5$
MD5 $1$
```

At the bottom of `/etc/shadow` we will target the kali user.

```
$ sudo cat /etc/shadow
...
king-phisher:*:18288:0:99999:7:::
kali:$6$jLA.1OwWM1uGyWTJ$xMETR7yrEky/pfF7bSpQ0i36A910R3JrE5c6uiuIQjQFF0gVCO7Hum.zI1lDsEZcjM07syG7B1ggxhtdAW9xN1:18288:0:99999:7:::
systemd-coredump:!!:18288::::::
...
```

We can see that the parts are seperated by colons (:), the first the username and the second is the hash. The `$6$` in this case identifies `SHA-512`.

Take the hash part, everything between the 2 colons (:) and paste into a new file on your cracking machine, lets say `kali.hash` I'm using `Git Bash` for windows on the cracking machine at this point. 

```
$ echo '$6$jLA.1OwWM1uGyWTJ$xMETR7yrEky/pfF7bSpQ0i36A910R3JrE5c6uiuIQjQFF0gVCO7Hum.zI1lDsEZcjM07syG7B1ggxhtdAW9xN1' > kali.hash
$ cat kali.hash
$6$jLA.1OwWM1uGyWTJ$xMETR7yrEky/pfF7bSpQ0i36A910R3JrE5c6uiuIQjQFF0gVCO7Hum.zI1lDsEZcjM07syG7B1ggxhtdAW9xN1
```

I won't cover hashcat installation here. To quickly test that everything is working create a file `kali.dict` and add one line
```
$ echo "kali" > kali.dict
$ cat kali.dict
kali
```

I have [hashcat](https://hashcat.net/hashcat/) 5.1.0 installed on a Windows 10 machine with a GTX 1080 NVIDIA graphics card. With [crackstation.net's](https://crackstation.net/crackstation-wordlist-password-cracking-dictionary.htm) small wordlist (64M PW's) `realhuman_phill.txt` installed under `/dictionaries`.

Run a quick test using `kali.dict`
```
$ ./hashcat64.exe -m 1800 -a 0 -o kali.pass kali.hash kali.dict
```

This should finish immediately and indicate that 1/1 Digests have been recovered. The original hash and cracked password is written to `kali.pass`

`hashcat` is smart enough to remember past results so you have to remove them for this final run.
```
$ rm hashcat.pot
```

Just to be sure, check your `realhuman_phill.txt` file for the password `kali`
```
$ grep '^kali$'  dictionaries/realhuman_phill.txt
kali
```

Now test with a real dictionary.
```
$ ./hashcat64.exe -O -m 1800 -a 0 -o kali.pass --remove kali.hash dictionaries/realhuman_phill.txt
```

Here is some info about the options. See [hashcat options](https://hashcat.net/wiki/doku.php?id=hashcat#options)

`-O` -> optimise OpenCl kernel (if you know that password is less than 32 char)
{: .notice--info}

`-m 1800` -> set hash type `sha512crypt $6$, SHA512 (Unix)`
{: .notice--info}

`-o` -> set attack mode as straight dictionary comparison
{: .notice--info}

`--remove` -> removes the hash from `kali.hash` when password sucessfully recovered.
{: .notice--info}

Depending on your GPU power this should eventually be cracked.

My testing took just over 5mins:
```
* Device #1: GeForce GTX 1080, 2048/8192 MB allocatable, 20 MCU
```
![alt text](\assets\images\hashcat-kali1.jpg)

