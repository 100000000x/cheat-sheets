# Linux Monitoring
```
apache2-utils
bash
bind-tools
bird
bridge-utils
busybox-extras
calicoctl
conntrack-tools
ctop
curl
dhcping
drill
ethtool
file
fping
httpie
iftop
iperf
iproute2
ipset
iptables
iptraf-ng
iputils
ipvsadm
jq
libc6-compat
liboping
mtr
net-snmp-tools
netcat-openbsd
netgen
nftables
ngrep
nmap
nmap-nping
openssl
py-crypto
py2-virtualenv
python2
scapy
socat
strace
tcpdump
tcptraceroute
termshark
tshark
util-linux
vim
websocat
```
basic
```console
ping
dig
ifconfig
tcpdump
```
curl
```console
-u
-A
-v
-X
-d
-c
-L
-b cookiejar
-c cookiejar
-b 'n1=v1;n2=v2'
Send Data
--data-binary @<filename>
-d <@filename>
-d <data>
-H <header>
-i
-l
-A 'User-Agent-Name'
6 cannot be resolved
7 could not connect
2 timed out
55 could not send
56 could not receive
-v / --verbose
-m / --max-time
-k / --insecure
-s
-S
```
check public ip
```console
ifconfig
curl https://ipinfo.io/ip
```
```
netstat check ports
```console
netstat -anutp
```
scan localhost
```
nmap 127.0.0.1
```
iptables enable localhost traffic
```console
sudo iptables -A INPUT -i lo -j ACCEPT
```
enable http, ssh, ssl ports
```console
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```
nmap scan target
```console
nmap 142.250.181.228
```
nmap scan host
```console
nmap www.google.com
```
nmap scan range
```console
nmap 142.250.181.1-24
```
nmap scan subnet
```console
nmap 142.250.181.228/13
```
nmap scan from txt
```console
nmap –iL textlist.txt
```
nmap scan/fast/all scan port/range/more target
```console
nmap –p/-F/-p- 80/1-200/-sV --version-intensity 0 to 9 142.250.181.228
```
nmap scan tcp/syn/udp ports/fastping/os target
```console
nmap -sT/-sS/-sU -p 80,130,255/sP -F/-A 142.250.181.228
```
