# 7ZIP
install 7zip command line
```console
sudo apt update
sudo apt upgrade
sudo apt install p7zip-full p7zip-rar
```
encrypt folder with pw
```console
cd folder
7z a -r -p ../zip .
```
decrypt
```console
7z e file
```
