# C Cheat Sheet Linux

_https://handsonnetworkprogramming.com/_
_https://hpbn.co/_

gcc
```console
sudo apt install gcc
gcc --version
gcc -g3 -o program program.c
gcc -std=c11 -g3 -o program program.c
gcc -std=c99 -g3 -o program program.c
gcc -ansi -pedantic -o program program.c
```
```console
make
```
```
gdb
```console
gdb program
help
run
quit
break
list
next
step
finish
cont
print
display
bt
```
c headers
```c
#include <assert.h>
#include <ctype.h>
#include <errno.h>
#include <float.h>
#include <limits.h>
#include <locale.h>
#include <math.h>
#include <setjmp.h>
#include <signal.h>
#include <stdarg.h>
#include <stddef.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
```
execvp
```
```
pipe
```
```
fork
```
```
child processes
```
```
interprocess communication
```
```
signals
```
```
