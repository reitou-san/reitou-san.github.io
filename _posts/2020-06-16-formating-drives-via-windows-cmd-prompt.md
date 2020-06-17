---
title: "Formatting drives via windows cmd prompt"
date: 2020-06-16T10:00:00
categories:
  - blog
tags:
  - windows
  - cmd prompt
  - rough cuts
---

I don't know what it is, but I'm constantly having to reformat Linux formated USB/SSD's etc on Windows. The problem with that is the standard GUI rejects working with special partitions (Linux swap, UEFI etc). So it has to be done via the Windows command prompt tool `diskpart`.

Firstly, run cmd.exe as administrator (right click, Run as administrator)
```cmd
1. C:\Windows\system32>diskpart
2. DISKPART> list disk
Correctly identify the target drive! e.g Disk 2
3. DISKPART> select disk 2
4. DISKPART> clean
5. DISKPART> create partition primary
6. DISKPART> format fs=ntfs
7. DISKPART> assign
Done!
```

