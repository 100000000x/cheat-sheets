# EMACS
```console
sudo apt install emacs
C- = CONTROL KEY
M- = ALT KEY / META
```
start emacs
```console
emacs
emacs -nw
```
start emacs with file
```console
emacs filename
```
start shell
```console
M-x shell
```
undo
```console
C-x u
```
quit emacs
```console
C-x C-c
```
quit input session
```console
C-]
```
save as
```console
C-x C-w
```
buffers and windows
```console
C-x C-f opens a new file
C-x b change between buffers
C-x o cycle between open panes
C-x C-b lists all open buffer
C-x k closes buffer
C-x 2 split  windows horizontally
C-x 3 split window vertically
C-x 1 quit all windows except open
C-0 close window
```
edit files with dired
```console
C-x d
M-x shell
ls or ls -la
m mark
u unmark
U unmark
C copy
R rename
D delete
+ create dir
! run selected
Q find replace regexp
Z compress/decompress selected
g refresh
^ go parent dir
> next sub dir
< previous sub dir
q quit window
```
emacs browser commands
```console
M-x eww
p eww-previous-url
r eww-forward-url
& eww-browse-with-external-browser
g eww-reload
w eww-copy-page-url
v eww-view-source
‘TAB’ - Next link
Shift+TAB - Previous link
‘b’ - Add bookmark
‘B’ - View bookmarks
‘d’ - Download link under point
‘l’ - Go back
‘r’ - Go forward
‘H’ - View history
‘g’ - reload the page
‘G’ - Enter a new URL or search
‘R’ - Attempt to improve readability
‘w’ - Copy the current URL
M-<RET> - Open link in new tab
‘s’ - Get a list of eww tabs

```
emacs for dev ops
```console
C-x C-f	find-file
C-x k	kill-buffer
C-x d	dired
C-x j	dired-jump
C-x C-b	list-buffers
```
emacs html helper
```console
https://www.irt.org/articles/js136/
```
copy, cut, paste
```console
M-w copy
C-w cut
C-y paste
```
delete word
```console
M-backspace
```
delete line
```console
C-k
```
select all
```console
C-x h
```
start selecting
```console
C-space key
arrow keys
enter key
```
search
```console
C-s type word
C-s next occurrence
C-r previous occurrence
C-g quit search at beginning
enter key quit search at cursor
```
find replace
```console
M-x query-replace
M-% (Alt and Shift+5 at the same time)
y replace this one
n skip to next
! replace all
Y replace all without verification
C-g quit
M-x replace-string
enter key to replace all
```
find replace regexp
```console
M-x query-replace-regexp
C-M-% (Control, Alt and Shift+5 at the same time)
y replace this one
n skip to next
! replace all
Y replace all without verification
C-g quit
M-x replace-regexp
enter to replace all
```
replace rectangle
```console
select rectangle
C-xrt
enter key
```
delete rectangle
```console
select rectangle
C-xrk
enter key
```
paste rectangle
```console
select rectangle
C-xry
enter key
```
