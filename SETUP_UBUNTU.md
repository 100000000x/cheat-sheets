# Install new Ubuntu distribution
```console
sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
sudo apt autoremove
sudo do-release-upgrade
```
# Remove and Update repositories
```console
sudo rm /etc/apt/sources.list.d/*
sudo add-apt-repository main
sudo add-apt-repository universe
sudo add-apt-repository restricted
sudo add-apt-repository multiverse
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```
# Install Gnome Tweaks, Tint All
```
https://extensions.gnome.org/
sudo apt install gnome-tweaks
https://extensions.gnome.org/extension/1471/tint-all/
```
# Install Vim, Tmux, Oh My Zsh, Emacs, gnome-tweaks, docker, docker-compose, pip
```
sudo apt update
sudo apt upgrade
sudo apt install vim
sudo apt install tmux
sudo apt install zsh
sudo apt install emacs
sudo apt install gnome-tweaks
sudo apt install docker
sudo apt install pip
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
https://docs.docker.com/compose/install/
```
# Install Atom.io Text Editor, Atom Script
```
Install Atom from website
Install Atom script package
update the grammar in  Atom's /script/lib/grammar/python.js for python3 scripts
open Atom via terminal
```console
atom .
```
# Debug Sound
```
sudo apt-get --purge remove linux-sound-base alsa-base alsa-utils
sudo apt-get install linux-sound-base alsa-base alsa-utils
```
