---
title: "Docker for Hackers"
date: 2020-06-01T10:00:00
categories:
  - blog
tags:
  - reverse engineering
  - docker
  - programming
  - rough cuts
---

Docker is a really useful tool for tesing out exploits. Usually, by the time I get around to creating a POC for an CVE, the software has been patched in some way. You can spin up a docker container real quick with the correct OS and base version and if it turns out you didn't quite get the right version you can quickly try again.

For example this one time I needed a specific version of Git to create a malicous submodule. GitHub was fully patched and could auto detected the exploit on commit so the POC had to be created locally. The docker container was approx. 100mb and took a few minutes to spin up ... as opposed to hunting down a full blown ISO installer or VM @ 4gb+

Here, we spin up the latest release debian or fedora 26 (which had the vulnerable versions of packages). The `-v` sets the current host machine directory to be mounted into the container at `/code`, this is useful for, say, sharing a cloned Git repo. instead of moving work back and forth.
```bash
$ docker run -it -v `pwd`:/code debian /bin/bash
$ docker run -it -v `pwd`:/code fedora:26 /bin/bash
```


Once the container is built and runs the `-it` flag gives plus `/bin/bash` gives you an interactive shell to the container. Then, depending on what you're doing install `vim` and `gcc` for building your exploits.
```bash
$ apt update && apt install vim gcc
$ <build stuff>
$ exit
```


Some other container commands.
```bash
docker ps -a
docker start <container id>
docker exec -it <container id> /bin/bash
docker container ls -a
docker container rm <container id>
```

