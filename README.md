Docker Image List
=================
### Notes
- for cicd, remove `-it` because it is not interactive
- ```bash
  #!/bin/bash
  # check if current script can access stdin file descriptor, if yes, enable iteractive mode in Docker
  # [Bash Redirection Fun With Descriptors | by Cindy Sridharan | Medium](https://copyconstruct.medium.com/bash-redirection-fun-with-descriptors-e799ec5a3c16)
  # [shell - What is "-t" in a bash script? - Stack Overflow](https://stackoverflow.com/questions/58086239/what-is-t-in-a-bash-script)
  # [bash - What does [ -t 1 ] check? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/389495/what-does-t-1-check)
  if  [ -t 0 ]; then
  	DOCKER_DEFAULT_OPTIONS="-it --rm"
  else
  	DOCKER_DEFAULT_OPTIONS="--rm"
  fi
  ```

### Build
- `Dockerfile`
  - ```bat
    docker build -t rsta2-circle .
    docker run --rm -it -v "%cd%/export:/home/ubuntu/circle/export" rsta2-circle
    # full docker run -it --rm -u $(id -u):$(id -g) --volume $PWD/tmp:/test --workdir /test $(KICAD_CLI_IMAGE) kicad-cli
    pause
    ```
- platform
  - ```bat
    docker build --platform=linux/amd64 -t mydebian .
    ```
- `docker-compose.dev.yml`
  - ```bat
    docker-compose --file docker-compose.dev.yml up --build && docker-compose --file docker-compose.dev.yml down
    pause
    ```
- [Day4：用簡單的例子來說明如何使用 Docker 指令 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10190921)

### Docker as command
- ```bash
  docker run --rm --name "${CONTAINER_NAME}" --mount type=bind,src=${PWD},target=/build -it "${IMAGE_NAME}" ./build.sh "$@"
  ```
### Docker waiting
- ```Dockerfile
  # container just waits, by default, actual builds can be done with `docker exec`
  CMD /bin/bash -c 'for ((i = 0; ; i++)); do sleep 100; done'
  ```
  
### Windows on qemu
- [dockur/windows: Windows inside a Docker container.](https://github.com/dockur/windows)
	- `docker run -it --rm -p 8006:8006  --cap-add NET_ADMIN --stop-timeout 120 dockurr/windows`

### macOS
- [dockur/macos: OSX (macOS) inside a Docker container.](https://github.com/dockur/macos)

### Just Linux
- on top of golang image
  ```
  docker run --rm -it --workdir="/root/" -p 8888:8888 -v "%~dp0:/root/" golang:latest bash
  ```
- Ubuntu
  ```
  docker run --rm -it ubuntu:latest bash
  ```

### Virtual framebuffer
- [bengreenier/docker-xvfb: Dockerfiles for running headless x11 apps 📦🤕✨](https://github.com/bengreenier/docker-xvfb)

### Mac OSX
- [sickcodes/Docker-OSX: Mac in Docker! Run near native OSX-KVM in Docker! X11 Forwarding!](https://github.com/sickcodes/Docker-OSX)

### OCS Inventory
- [OCS Inventory Docker image - OCS Inventory Documentation](https://wiki.ocsinventory-ng.org/13.Docker-documentation/Using-the-docker-image/)
	- ```bash
	  docker run -p 9880:80 -p 9443:443 --name my-ocs -e OCS_DB_NAME=DB_NAME -e OCS_DB_SERVER=DB_HOST -e OCS_DB_PORT=DB_PORT -e OCS_DB_USER=DB_USER -e OCS_DB_PASS=DB_PASS -itd ocsinventory/ocsinventory-docker-image:latest
	  ```
  
### OpenSSL
- ```Dockerfile
  from alpine/openssl as ssl
  run mkdir /ssl && openssl req -x509 -newkey rsa:2048 -sha256 -days 36500 -nodes -keyout /ssl/key -out /ssl/cert -subj '/CN=hubs'
  ```
- ```Dockerfile
  from node:lts as build
  run mkdir certs && openssl req -x509 -newkey rsa:4096 -sha256 -days 36500 -nodes -keyout certs/key.pem -out certs/cert.pem -subj '/CN=dialog'
  ```
### MS SQL Server on Linux
```
docker run --rm -it -e ACCEPT_EULA=Y -e SA_PASSWORD=P@ssw0rd -p 1433:1433 mcr.microsoft.com/mssql/server:2019-latest
```

### KiCad
```
docker run --rm -v $HOME/src/:/local/src kicad/kicad:8.0.6 kicad-cli version
```

### VNC-ready Ubuntu
```
docker pull welkineins/ubuntu-xfce-vnc-desktop
docker run -i -t -p 5900:5900 welkineins/ubuntu-xfce-vnc-desktop
```
### [Web-VNC-ready Ubuntu](https://github.com/fcwu/docker-ubuntu-vnc-desktop) / [dirkarnez/ubuntu-desktop-lxde-vnc-action](https://github.com/dirkarnez/ubuntu-desktop-lxde-vnc-action)
```
docker pull dorowu/ubuntu-desktop-lxde-vnc
docker run -p 6080:80 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc
Browse http://127.0.0.1:6080/
```

### Enable VPN
````
docker run --cap-add=NET_ADMIN -p 6080:80 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

mkdir /dev/net -pv
mknod /dev/net/tun c 10 200
chmod 666 /dev/net/tun

Dockerfile
FROM dorowu/ubuntu-desktop-lxde-vnc

RUN mkdir /dev/net -pv && \
 mknod /dev/net/tun c 10 200 && \
 chmod 600 /dev/net/tun
````

### [Oracle Express Edition 11g on Ubuntu](https://github.com/wnameless/docker-oracle-xe-11g), removed from DockerHub
```
docker pull wnameless/oracle-xe-11g
docker run -d -p 1521:1521 wnameless/oracle-xe-11g

hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
```

### Oracle Express Edition 11g on Ubuntu
```
docker pull epiclabs/docker-oracle-xe-11g
docker run -d -p 1521:1521 epiclabs/docker-oracle-xe-11g

hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
```
### [Oracle 12c Standard Edition](https://hub.docker.com/r/laboratoriobridge/oracle-12c)
```
docker pull laboratoriobridge/oracle-12c
docker run -d -p 8888:8080 -p 1521:1521 laboratoriobridge/oracle-12c

hostname: localhost
port: 1521
sid: xe
service name: xe
username: system / sys (SYSDBA)
password: oracle
```

### [Fine Report](https://github.com/juglans/finereport)
```
docker pull juglans/finereport
docker run -d -p 8080:8080 juglans/finereport
```

### MariaDB
```
docker pull mariadb
docker run --rm -it -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=default mariadb
# -e TZ=Asia/Hong_Kong
```

### [Node-RED](https://nodered.org/)
```
docker pull nodered/node-red-docker
docker run -it -p 1880:1880 nodered/node-red-docker
````

### [Jupyter Notebook](https://github.com/dirkarnez/docker-jupyter-notebook)

### [Apache PHP](https://github.com/dirkarnez/docker-php-apache)

### Nvidia
- [NVIDIA/nvidia-docker: Build and run Docker containers leveraging NVIDIA GPUs](https://github.com/NVIDIA/nvidia-docker)

### Machine Learning
- [ContinuumIO/docker-images: Repository of Docker images created by Continuum Analytics](https://github.com/ContinuumIO/docker-images)

### OSes
- [Dockur](https://github.com/dockur)
	- [dockur/windows: Windows inside a Docker container.](https://github.com/dockur/windows)
	- [dockur/windows-arm: Windows for ARM in a Docker container.](https://github.com/dockur/windows-arm)
	- [dockur/macos: OSX (macOS) inside a Docker container.](https://github.com/dockur/macos)
	- [dockur/samba: Samba SMB server in a Docker container.](https://github.com/dockur/samba)
	- [dockur/chrony: 🕒 chronyd NTP server in a Docker container.](https://github.com/dockur/chrony)
	- [dockur/umbrel: umbrelOS inside a Docker container.](https://github.com/dockur/umbrel)

### Healthcheck
- `HEALTHCHECK CMD wget --no-check-certificate --no-verbose --tries=1 --spider https://localhost:4000/stream-offline.png`

### Cross compilation
- [dockcross/dockcross: Cross compiling toolchains in Docker images](https://github.com/dockcross/dockcross)
- [VideoLAN / docker-images-aarch64 · GitLab](https://code.videolan.org/videolan/docker-images-aarch64)
- [VideoLAN / docker-images-armv7 · GitLab](https://code.videolan.org/videolan/docker-images-armv7)

### torrent
- [crazy-max/docker-qbittorrent: qBittorrent Docker image based on Alpine Linux](https://github.com/crazy-max/docker-qbittorrent)

### Awesome
- [dev-cafe/docker-images: Docker images for fun and for profit](https://github.com/dev-cafe/docker-images)

### Docker tricks
- Set Timezone `RUN echo "Asia/Shanghai" > /etc/timezone;` 
- Set hosts file, must be in one line `CMD echo "ip hostname" >> /etc/hosts && ./you-application`
- Set rights `RUN chmod -R 777 /root`

### Common Dockerfile commands
* `RUN` commands triggers while building the docker image
* `CMD` commands triggers while launching the created docker image
- sudo
	- ```Dockerfile
		# Create ubuntu user with sudo privileges
		RUN useradd -ms /bin/bash ubuntu && \
		usermod -aG sudo ubuntu
		# New added for disable sudo password
		RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

		# Set as default user
		USER ubuntu
		```
### Common Docker CLI commands
 - `docker system prune -a --volumes` delete everything
 - [Docker常用操作集合_docker-entrypoint-initdb.d能挂载configmap定义的shell脚本吗-CSDN博客](https://blog.csdn.net/weixin_64632836/article/details/141871750)
 
### Common Dockerfile snippets
```Dockerfile
RUN apt-get update -y \ 
&& apt-get -y --no-install-recommends install \
   build-essential \
   libgomp1 \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```
```Dockerfile
# USERID should be same as the current user.
ARG USERID
ARG USERNAME=ci

ENV DISPLAY=":0"

RUN useradd --create-home --no-user-group -u $USERID $USERNAME -s /bin/bash && adduser $USERNAME sudo

RUN apt-get update && \
	apt-get install -y --no-install-recommends ansible sudo && \
	rm -rf /var/lib/apt/lists/* && \
    apt-get clean 
```

### Reference
- https://github.com/arville27/ppe/blob/master/Dockerfile
- https://github.com/qbittorrent/docker-qbittorrent-nox
- https://github.com/arville27/ppe/blob/master/docker-compose.yml
