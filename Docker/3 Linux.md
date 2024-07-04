# Linux
## Linux Distribution
- Linux is open source software. For this reason many people created own version of Linux. These version called Linux distributions.
- Each of distribution specialize to fit specific tasks.
	- running servers
	- Desktop computers, mobile phones
- examples for Linux distribution
		- Ubuntu
		- Debian
		- Alpine (small linux distribution)

## Run ubuntu using docker image
- [go to docker hub](https://hub.docker.com/) and search for ubuntu.
- go to terminal and `docker run ubuntu`. If you have image locally docker is going to start container with image. If it isn't first docker pull the image and continue.
- `docker ps` - list of running processors or containers
- `docker ps -a` - all running and stop containers
- we have to run ubuntu docker image in interactive mode to use linux `docker run -it ubuntu`. Here `it` stand for interactive
- Now we can see "shell".
	![](assets/Pasted%20image%2020240629094600.png)
- Shell is program that take command and pass it to the operating system
- `root@dd94909920fa:/#` 
	- `root`- login as root user and it is highest privilege user.
	- `dd94909920fa`- name of the machine. automatically generate by docker
	- `/` represent root directory 
	- `#` indicate login as root user. If it is normal user it will show as `$`.
- In this shell we can execute bunch of commands
  - ex- 
  	![](assets/Pasted%20image%2020240629095201.png)
  - `whoami` shows current user 
  	![](assets/Pasted%20image%2020240629095233.png)
  - `echo $0` shows location of shell program
  	![](assets/Pasted%20image%2020240629095501.png)
	  - bin is a director and inside the directory there is program called 
bash. Bash is enhance version of shell program.
  - `history` we can see command history
		![](assets/Pasted%20image%2020240629113514.png)
  - replay command from history using `!`"command number"
		![](assets/Pasted%20image%2020240629113717.png)

## Difference between Linux and Windows
1. Linux use forward slash`/` to separate folders and directories. But windows use back slash `\`.
2. Linux is case sensitive operating system
	- ex- Here we use `Echo` intend of `echo`
		![](assets/Pasted%20image%2020240629113009.png)
	