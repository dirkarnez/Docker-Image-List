## Docker Image List

### MS SQL Server on Linux
```
docker pull microsoft/mssql-server-linux:latest
docker run -e ACCEPT_EULA=Y -e SA_PASSWORD=<Password here> -p 1433:1433 -d microsoft/mssql-server-linux:latest
```
