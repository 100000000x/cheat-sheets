# Tmux Cheat Sheet
```
sudo apt update
sudo apt install tmux
sudo apt install vim
sudo apt install curl wget git
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
tmux commands
```
tmux new -s SESSION
Ctrl + b c
Ctrl + ,
Ctrl + b %
Ctrl + b o
Ctrl + b p
Ctrl + b '
Ctrl + b d
Ctrl + b (
Ctrl + b )
tmux kill-ses -t SESSION
tmux kill-session -a
tmux kill-session -a -t SESSION
tmux attach -d
tmux ls
tmux list-sessions
tmux a -t SESSION
tmux at -t SESSION
tmux attach -t SESSION
tmux attach-session -t SESSION
Attach to a session with the name SESSION
Ctrl + b $
Ctrl + b ,
Ctrl + b s
Ctrl + b w
```
