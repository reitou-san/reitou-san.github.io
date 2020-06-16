---
title: "Simple Buffer Overflows"
date: 2020-05-16T09:32:00
categories:
  - blog
tags:
  - reverse engineering
  - buffer overflow
  - stack smashing
  - programming
  - rough cuts
---

At the moment this article is just a brief outline of creating a simple buffer overflows and breaking them.


By default `gcc` stack smashing is `OFF` by `DEFAULT`. This is a feature that allows automatic protection against `stack smashing`, the main attack vector of buffer overflows. Try compiling with `gcc` defaults and retry with the `no` flag listed below.


The `gcc` flags for `yes` and `no` are listed here.
```
-fstack-protector
-fno-stack-protector
```


Here is an example of very simple `c` code that is vulnerable to a `stack` overflow.

```c
// stack.c
#include <string.h>

int main(int argc, char** argv)
{
  char aBuffer[10];
	strcpy(aBuffer, argv[1]);
}
```

```bash
$ gcc stack.c -o stack
$ ./stack $(python -c 'print "A"*9')
$ ./stack $(python -c 'print "A"*19')
```

And here is an example of very simple `c` code that is vulnerable to a `heap` overflow.

```c
// heap.c
#include <string.h>
#include <stdio.h>

void main(int argc, char** argv)
{
	char* buffer=malloc(20);
	strcpy(buffer, argv[1]);
	free(buffer);
}
```

```bash
$ gcc heap.c -o heap
$ ./heap $(python -c 'print "A"*20')
$ ./heap $(python -c 'print "A"*1000')
```

