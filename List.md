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

### [Oracle Express Edition 11g on Ubuntu](https://github.com/wnameless/docker-oracle-xe-11g)
```
docker pull wnameless/oracle-xe-11g
docker run -d -p 1521:1521 wnameless/oracle-xe-11g

hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
```
