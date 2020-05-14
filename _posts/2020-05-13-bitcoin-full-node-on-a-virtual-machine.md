---
title: "Bitcoin Full-Node on a Virtual Machine"
date: 2020-05-13T10:56:00
categories:
  - blog
tags:
  - bitcoin
  - virtual machines
  - rough cuts
---

```
*rough cut notes*
```

So I'll start off and say that this is an unsual setup. After many years of experimenting running Bitcoin Core on different platforms I'm at the point where my restricting factor is an ext4 formatted USB drive that contains the full Bitcoin ledger.

Yes! I went about running on a Raspberry PI like everyone else but found the mess of extra hardware and maintenance an inconvience. Also many guides recommend a minimum 2Gb of RAM and 512GB storage for a Raspberry PI setup. My experimenting found you really need at least 4GB if you don't want the system to be so slow. 1-2GB is ok for a set and forget blackbox. If that is what you want I recommend following a Raspberry Pi 4 guide such as [kdmukai's](https://github.com/kdmukai/raspi4_bitcoin_node_tutorial) guide since a Raspberry PI now has 4GB RAM. You can buy starter kits on eBay and just need to get USB storage. These days you really need a minimum of 4GB RAM and a minimum of 1TB of storage to work comfortably.

So, lets say you want to experiment with running a Node and don't want to buy the Raspberry Pi hardware right now, but you do have a Windows desktop and a spare USB 1TB drive. This guide will get you started with running a linux node in a VM on Windows 10 and sync the ledger. This way the VM is disposable and all the hardwork of syncing the ledger is kept, ready for direct transplant into a Raspberry PI setup.

I've choosen Fedora Desktop Xfce because it is very lightweight on requirements and yet gives you a decent desktop to work with.

<br>
Items needed:
- A Windows 10 PC
- 1TB USB mass storage drive
- [Virtual Box](https://www.virtualbox.org/wiki/Downloads) software
- [Fedora 32 Xfce Desktop](https://spins.fedoraproject.org/xfce/download/index.html) iso
- [Bitcoin Core](https://bitcoin.org/en/download) software (downloaded within VM after it is built)

<br>
Steps:
1. Install Virtual Box
2. Create new VM, Linux-Fedora64, 4Gb RAM, 80Gb storage dynamic, bridged adapter, 2x CPUs & USB 3.0 Controller
3. Add iso, install add local user and a root password
4. Shutdown, remove iso, startup
5. Add USB storage, Virtual box -> devices -> usb -> enable external USB
6. Login as user, goto desktop and open up the drive (it then auto mounts), get location from File Manager (/run/media/user/USBname)
7. Open root terminal
8. Download bitcoin core linux + checksum:
```
wget https://bitcoin.org/bin/bitcoin-core-0.19.1/bitcoin-0.19.1-x86_64-linux-gnu.tar.gz
wget https://bitcoin.org/bin/bitcoin-core-0.19.1/SHA256SUMS.asc
```
9. verify check sum
```
$ sha256sum -c SHA256SUMS.asc -> look for OK
```
10. extract and install to system
```
tar xzf bitcoin-0.19.1-x86_64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-0.19.1/bin/*
```
11. run up qt interface
```
/usr/local/bin/bitcoin-qt
```
12. point node software to USB root + /bitcoin and DONT prune (e.g. /run/media/user/USBname/bitcoin)
13. watch for a while as it creates stuff and syncs headers, if any segfaults restart. Check USB /bitcoin to see files being created.

This will sync for a long ... long time, unless you are transplanting a backup of the ledger then it shows how much to catch up on, which still take a long ... long time.
Don't forget to add the USB drive after a VM restart! (a shutdown, then virtual box startup)

<br>
Improvements
```
+how to run as daemon
+auto UUID USB external drive to static location
```
