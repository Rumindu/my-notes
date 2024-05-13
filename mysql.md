## Setup mysql using docker image

#### Working way link- https://hevodata.com/learn/docker-mysql/

- Access mysql client in WSL - `docker run -it mysql /bin/bash` In here create docker image of mysql client.
- then type `mysql -h 172.17.0.2 -u root -p`  (We can see this ip address from view `details of docker container -> Inspect -> Networks.IPAddress` )
- Finally enter the password


## Setup mysql in WSL

- We need to configure mysql in WSL to login **root** user without having ***sudo*** permission.
	1.  `sudo service mysql start`
	2. `sudo mysql_secure_installation` 1 & 2 from [Microsoft documentation of install mysql in wsl](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)
	3. then go to mysql console and `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';`
	4. `FLUSH PRIVILEGES;`
### Commands are-
1. `SHOW DATABASES;`
![](assets/Pasted%20image%2020240212140749.png)
2. `USE mysql;`
3. `SHOW TABLES;`
4. `DESC user;`
5. `SELECT user, plugin FROM user;`
	![](assets/Pasted%20image%2020240212140945.png)
	here we need to update root password plugin like this .

