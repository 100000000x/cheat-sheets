# VIM Cheat Sheet
```console
sudo apt install zsh
zsh
sudo apt install vim
vim file_name
```
meta command
```
esc key
```
window movement
```console
gg
G
CTR+u
CTR+d
k
j
h
l
w
e
b
/forward
?backward
#
n
N
0
$
```
copy paste delete undo redo
```console
c
C
w
cw
yy
p
11yy
x
s
r
D
dd
22dd
u
4u
CTRL+R
ZZ
d 0
d $
d G
d ap
```
write
```console
i
a
I
A
o
O
```
last line commands
```console
:wq
:q!
o
:r append.txt
:sh
:s/old/new/
:s/old/new/g # entire row
:1,$s/old/new # 1st each column
:%s/old/new/g # each column, each row
:%s/old/new/gc # each column, each row, safe mode
:h
:make
:e filename
:set
:! zsh
exit
```
vim misc
```
cd ~
vi .vimrc
jobs
ps -ef | grep vim
set -o vi
set -o -emacs
vim -r file
:w file2
:q!
diff file file2
rm .file.swp file2
rm .file.swp
mv file2 file
```
