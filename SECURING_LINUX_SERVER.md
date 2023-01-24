# Securing Linux

## Linux Hardening Heuristics
_Root user is not avaliable for execution_
_Disable root SSH_  
_Domain name SPOC is load balancer_  
_Unused ports are deactvated_  
_User content is on different domain_  
_Shelf Object Relational Mapper (ORM)_  
_Shelf HTML template library (ORM)_  
_Shelf CSRF Tokens_  
_Use DNF whenever possible_  
_1 VM = 1 microservice, 1 Container = 1 service_  

## Flow
1. 1/d backup ACID
2. root pw never used - set with head dev/uurandom | uunicode > text.txt | zip...
3. only ssh access to sudo user
4. uwf only 80, 443 open + cloud firewall
5. fail2ban -1 after 10 tries
6. run container rootless / only sudo user group
7. FROM x as build, FROM y as production build, minimal distro alpine
8. USER runs all in container
10. secrets, keys all only in .env 
11. csrf tokens, hsts, web app settings  
12. fake email sign up checks, password checks, 2fa, token auth, user system auth, fingerprints 
13. CDN redirects, load balancers, timeouts, IP block 
14. CI/CD sec checks, health checks, dependabots  

Ubuntu
```
vi /etc/ssh/sshd_config
PasswordAuthentication no
ufw default allow outgoing
ufw default deny incoming
ufw allow ssh
ufw allow http
ufw allow https
ufw enable
ufw status
scp -r /home/mac/Desktop/app user@x.x.x.x.:/

vi /etc/fail2ban/jail.local

[DEFAULT]
bantime = -1
findtime = 7d
maxretry = 5
banaction = iptables-multiport

[sshd]
enabled = true

[ssh]
enabled = true

systemctl start fail2ban
systemctl enable fail2ban
systemctl status fail2ban
fail2ban-server --version
fail2ban-client status sshd
fail2ban-client status <jail_name>
fail2ban-client set <jail_name> unbanip <ip_address>
fail2ban-client get <JAIL_NAME> ignoreip
fail2ban-client set <JAIL_NAME> delignoreip <IP_Address>
iptables -n -L
last
lastb

adduser appuser
usermod -aG sudo appuser
su - appuser

```
Centos
```
sudo dnf groupinstall "Development tools"
```
users
```
adduser newsudouser
usermod -a -d -m -G wheel newsudouser
passwd newsudouser secret
grep newsudouser /etc/passwd
deluser -f -r newsudouser
su -
```
sshd
```
vi /etc/ssh/sshd_config
PermitRootLogin yes
PermitEmptyPasswords yes
PasswordAuthentication no
PubkeyAuthentication yes
systemctl restart sshd
systemctl enable sshd
```
ssh keys
```
ssh-keygen -b
ssh-copy-id newuser@ip_address
```
iptables
```
iptables -L
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 7822 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

iptables -P INPUT DROP

iptables-save > /etc/sysconfig/iptables
iptables-restore < /etc/sysconfig/iptables
iptables-restore -n < /etc/sysconfig/iptables

dnf install iptables-services
systemctl start iptables
systemctl enable iptables
service iptables save
```
fail2ban
```
dnf upgrade
dnf install epel-release -y
dnf install fail2ban -y
vi /etc/fail2ban/jail.local
[DEFAULT]
ignoreip = Your-server-ip
bantime = 1d
findtime = 1d
maxretry = 5
banaction = iptables-multiport
backend = systemd
[sshd]
enabled = true
systemctl start fail2ban
systemctl enable fail2ban
systemctl status fail2ban
```
