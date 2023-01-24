# Docker - Kubernetes Administration

## Some Resources:
- https://docs.docker.com/
- https://docs.docker.com/compose/install/
- https://docs.docker.com/compose/compose-file/
- https://docs.docker.com/storage/volumes/
- https://hub.docker.com/_/postgres/
- https://github.com/wagoodman/dive/releases
- https://github.com/nicolaka/netshoot
- https://github.com/bcicen/ctop
- https://github.com/GoogleContainerTools/distroless
- https://containerd.io/
- https://kubernetes.io/
- https://semver.org/
- https://opencontainers.org/
- https://docs.microsoft.com/en-us/windows/wsl/

## Install Docker and Docker Compose Centos

```console
# first always purge all legacy containerization files
sudo yum remove docker \
                 docker-client \
                 docker-client-latest \
                 docker-common \
                 docker-latest \
                 docker-latest-logrotate \
                 docker-logrotate \
                 docker-engine
sudo yum remove docker-ce docker-ce-cli containerd.io
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```
install docker
```console
dnf groupinstall "Development tools"
sudo yum install -y yum-utils
sudo yum-config-manager \
   --add-repo \
   https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
```
docker compose
```console
CHANGE URL TO NEWEST VERSION FROM
https://github.com/docker/compose/releases/
https://docs.docker.com/compose/install/
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo usermod -aG docker username
docker–compose --version
```
docker dive
```console
https://github.com/wagoodman/dive/releases
# debian
sudo apt install ./dive_X.X.X_linux_amd64.deb
# centos
rpm rpm -i dive_X.X.X_linux_amd64.rpm
```
```
docker debugging
```console
docker inspect
dive IMAGENAME
docker run --name netshoot --rm -it --network custombridge nikolaka/netshoot /bin/bash
docker exec -ti container /bin/bash
docker start -i IMAGENAME
dive IMAGENAME
$PWD/pgtest.dump:/docker-entrypoint-initdb.d/init.sql:ro
pgdata:/var/lib/postgresql/data
docker exec -ti POSTGRES_CONTAINER pg_dump -U postgres postgres > pgtest.dump
```
docker image container network volume compose
```console
docker image rm / ls -a / create / inspect
docker container rm / ls -a / create / inspect
docker volume rm / ls / create / inspect
docker network rm / ls / create / inspect
docker logs -f CONTAINERNAME
docker stop CONTAINERNAME
docker start CONTAINERNAME
docker exec -ti CONTAINERNAME bash
docker run --rm --name CONTAINERNAME IMAGENAME
docker run --rm --name myhttpd -p 9090:80 httpd:latest
docker run --name mypg postgres:12
docker run --name mypg --rm -e POSTGRES_PASSWORD=postgres -v $PWD/pgdata:/var/lib/postgresql/data  postgres:12
docker run --name mypg --rm -e POSTGRES_PASSWORD=postgres -v $PWD/pgtest.dump:/docker-entrypoint-initdb.d/init.sql:ro  -v pgdata:/var/lib/postgresql/data -p 127.0.0.1:5432:5432  postgres:12
docker exec -ti pgtest pg_dump -U postgres postgres > pgtest.dump
docker start -a mypg
docker rmi IMAGENAME
docker volume rm pgdata
docker ps -a
docker history
docker stats
docker info
docker container ls -a
docker container ls --filter "status=exited"
docker container ls -a --filter "ancestor=image_name"
docker container ls -a -q --filter "ancestor=ubuntu"
docker container ls -a-n=-1
docker container ls -a-s
docker container NAME stop
docker container prune
docker commit --help
docker-compose rm --all &&
docker-compose build --no-cache &&
docker-compose up -d --force-recreate &&
docker-compose up -d
docker-compose down && docker-compose up --build -d && docker-compose logs --follow
docker-compose -f /././././docker-compose.module.yml up --build -d
docker-compose -f docker-compose.postgres.yml exec postgres bash
docker-compose logs -f
docker-compose down --volumes
```
docker network
```console
docker network ls
docker network create dock-net
docker network prune
docker network ls
docker network inspect bridge
docker network create custombridge
ip a | grep ens18
ps aux | grep docker
docker network create -d macvlan --subnet 192.168.0.24 --gateway 192.168.0.1 --ip-range  192.168.0.253/32 -o parent=ens18 custommacvlan
docker run --name netshoot --rm -it --network custommacvlan nikolaka/netshoot /bin/bash
docker run -rm -d --name ngnix2 --network custommacvlan --ip 192.168.0.202 ngnix
```
linux
```console
id
ps
ps ef
ps alx
ps aux
kill
kill -9
du
df -h
df -i
ps
lscpu
lshw
stat
cat /etc/hostname
cat /etc/passwd
cat /etc/issue
cat /etc/group
cat /proc/meminfo
ls /sys/fs/cgroup
ls -la /var/run/docker*
chroot folder /bin/bash
```
docker cleanup
```
#!/bin/bash

# Install jq thus:
# sudo apt-get install -y jq


# LOCKFILE=/tmp/block_file
#
# if ( set -o noclobber; echo "$$" > "$LOCKFILE") 2> /dev/null;
# then
#     trap 'rm -f "$LOCKFILE"; exit $?' INT TERM EXIT
#
# while true; do
#   DATE=`date '+%Y-%m-%d'`;

docker-compose -f docker-compose.yml down -v && docker container prune -f && docker network prune -f && docker rmi -f $(docker images -a -q) && docker images -a | awk '{print $3}' | xargs docker rmi && docker ps -a | grep Removal | cut -f1 -d' ' | xargs -rt docker rm  2>&1 >/dev/null | grep "dataset does not exist" |  awk '{print $(NF-4)}' | sed "s/'//g" | cut -f1 -d':' |  xargs -L1 sh -c 'for arg do sudo zfs destroy -R "$arg"; sudo zfs destroy -R "$arg"-init ; sudo zfs create "$arg" ; sudo zfs create "$arg"-init ; ...; done' _ ; docker ps -a | grep Removal | cut -f1 -d' ' | xargs -rt docker rm 2>&1 >/dev/null

stuck=$(docker ps -a | grep Removal | cut -f1 -d' ')
echo "$stuck"
for container in $stuck; do
	zfs_path=$(docker inspect "$container" | jq -c '.[] | select(.State | .Status == "dead")|.GraphDriver.Data.Dataset')
	zfs_path=$(echo "$zfs_path"|tr -d '"')
	sudo zfs destroy -R "$zfs_path"
	sudo zfs destroy -R "$zfs_path"-init
       	sudo zfs create "$zfs_path"
       	sudo zfs create "$zfs_path"-init
	docker rm "$container"
done

# systemctl stop stop docker                                                          
# zfs list -H -o name -t snapshot | grep docker                                       
# zfs list -H -o name -t snapshot | grep docker | xargs -n1 sudo zfs destroy -R       
# sudo systemctl start docker

# docker-compose -f docker-compose.yml up --build

# # sleep 10 hours
#   sleep $((10 * 60 * 60))
# done
#
# rm -f "$LOCKFILE"
#    trap - INT TERM EXIT
#
# else
#    echo "Warning. Script is already running!"
#    echo "Block by PID  $(cat $LOCKFILE) ."
#    exit
# fi
#
# # nohup ./nohup.this.ampers.sh &
# # kill -11 thisPID

```
dockerfiles
```
# docker build . DOCKER CLI -> DOCKER DAEMON
# .dockerignore

# DECLARE IMAGE SOURCE 1. LAYER HASH / SAVES TO HDD
FROM ubuntu:18.04

# CHANGE DATA OF IMAGE 2. LAYER HASH / SAVES TO HDD
RUN apt-get update && apt-get upgrade -y \
      && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
           apache2 \
           curl \
           ca-certificates \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/* \
      && rm -rf /tmp/*

# CHANGE DATA OF IMAGE 3. LAYER HASH SAVES TO HDD
COPY httpd-foreground /usr/local/bin/

# CHANGE METADATA / IMAGE MANIFEST OF IMAGE 4., 5. / THIS IS THE DOCKER INSPECT METADATA
EXPOSE 80
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

# CONTAINER RUNTIME: ADDS READ WRITE LAYER

```
docker compose files
```
version: '3'

services:
  postgres:
    image: postgres:12
    restart: always
    volumes:
      - pgdata:/var/lib/postgresql/data # named volume, volume at /var/lib/docker/volumes
      - $PWD/pgtest.dump:/docker-entrypoint-initdb.d/init.sql:ro # bind mount mounts db inside to be run as init script, volume located where declared
    environment:
      - POSTGRES_PASSWORD=postgres
    ports:
      - 127.0.0.1:5432:5432

volumes:
  pgdata:
```
install kubernetes
```
```
