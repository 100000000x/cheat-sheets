# tcpdump and tshark

_use www.explainshell.com_

install zsh and tshark
```console
sudo apt update
sudo apt upgrade
sudo apt install zsh
sudo apt install tshark
```
tcpdump
```
ip a
tcpdump -i <interface>
tcpdump -i <interface> src port 80 or dst port 80 -w port-80-recording.pcap
tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-fin) != 0'
tcpdump "tcp port 8081 and (tcp[((tcp[12] & 0xf0) >>2)] = 0x16) && (tcp[((tcp[12] & 0xf0) >>2)+5] = 0x01)" -w client-hello.pcap
tcpdump "tcp port 8081 and (tcp[((tcp[12] & 0xf0) >>2)] = 0x16) && (tcp[((tcp[12] & 0xf0) >>2)+9] = 0x03) && (tcp[((tcp[12] & 0xf0) >>2)+10] = 0x03)"
tcpdump "tcp port 8081 and (tcp[((tcp[12] & 0xf0) >>2)] = 0x17) && (tcp[((tcp[12] & 0xf0) >>2)+1] = 0x03) && (tcp[((tcp[12] & 0xf0) >>2)+2] = 0x03)" -w appdata.pcap
tcpdump "tcp port 8081 and (tcp[((tcp[12] & 0xf0) >>2)] = 0x15) || (tcp[((tcp[12] & 0xf0) >>2)] = 0x21)" -w error.pcap
```
tshark
```
tshark-i <interface>
tshark port-80-recording.pcap
tshark -i any -Y 'http.request.method == "GET"' -T fields -e http.request.method -e http.request.uri -e ip.dst
```
