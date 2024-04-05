## Setup mysql using docker image

#### Working way link- https://hevodata.com/learn/docker-mysql/

- Access mysql client in WSL - `docker run -it mysql /bin/bash` In here create docker image of mysql client.
- then type `mysql -h 172.17.0.2 -u root -p`
- Finally enter the password


## Setup mysql in WSL

- We need to configure mysql in WSL to login **root** user without having ***sudo*** permission.
### Commands are-
1. `SHOW DATABASES;`
![](assets/Pasted%20image%2020240212140749.png)
2. `USE mysql;`
3. `SHOW TABLES;`
4. `DESC user;`
5. `SELCT user, plugin FROM user;`
	![](assets/Pasted%20image%2020240212140945.png)
	here we need to update root password plugin like this .

