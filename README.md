Docker Image List
=================

### Just Linux (on top of golang image)
- ```
  docker run --rm -it --workdir="/root/" -p 8888:8888 -v "%~dp0:/root/" golang:latest bash
  ```

### Mac OSX
- [sickcodes/Docker-OSX: Mac in Docker! Run near native OSX-KVM in Docker! X11 Forwarding!](https://github.com/sickcodes/Docker-OSX)

### MS SQL Server on Linux
```
docker pull microsoft/mssql-server-linux:latest
docker run -e ACCEPT_EULA=Y -e SA_PASSWORD=<Password here> -p 1433:1433 -d microsoft/mssql-server-linux:latest
```

### VNC-ready Ubuntu
```
docker pull welkineins/ubuntu-xfce-vnc-desktop
docker run -i -t -p 5900:5900 welkineins/ubuntu-xfce-vnc-desktop
```
### [Web-VNC-ready Ubuntu](https://github.com/fcwu/docker-ubuntu-vnc-desktop)
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
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password mariadb
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

### Cross compilation
- [dockcross/dockcross: Cross compiling toolchains in Docker images](https://github.com/dockcross/dockcross)
### Docker tricks
- Set Timezone `RUN echo "Asia/Shanghai" > /etc/timezone;` 
- Set hosts file, must be in one line `CMD echo "ip hostname" >> /etc/hosts && ./you-application`
- Set rights `RUN chmod -R 777 /root`

### Common Dockerfile commands
* `RUN` commands triggers while building the docker image
* `CMD` commands triggers while launching the created docker image

### Common Docker CLI commands
 - `docker system prune -a --volumes` delete everything
 
### Common Dockerfile snippets
```
RUN apt-get update -y \ 
&& apt-get -y --no-install-recommends install \
   build-essential \
   libgomp1 \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```
