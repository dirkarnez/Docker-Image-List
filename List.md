## Docker Image List

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

### Common Dockerfile commands
* `RUN` commands triggers while building the docker image
* `CMD` commands triggers while launching the created docker image
