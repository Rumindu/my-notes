spring boot learning materials yt channel [Daily Code Buffer](https://www.youtube.com/@DailyCodeBuffer/featured) 
# Spring boot-PSR part 1
- Initiate spring boot project.
	1. Spring Initializer
	2. New project from IntelliJ

1. Spring Initializer
- got to [Spring Initializer](https://start.spring.io/)for access Spring Initializer GUI
  ![](assets/Pasted%20image%2020240715143328.png)
- Keep all configuration in default state except choose `Maven` as project build tool
	![](assets/Pasted%20image%2020240715143609.png)
- Then Add dependencies 
	![](assets/Pasted%20image%2020240715144033.png)
- Dependencies for Simple spring boot app
	- Spring Web
	- jpa
	- mysql driver
	- h2 - fast in memory for temporally database
- After added dependencies can see like this 
  ![](assets/Pasted%20image%2020240715200738.png)
- In react project we can see installed dependencies on `package.json` file. Here also we can see installed dependencies on `porn.xml` file
  ![](assets/Pasted%20image%2020240715200940.png)
- `porn.xml`
	![](assets/Pasted%20image%2020240715201002.png)
- If all good you can download the package.
2. We can follow similar path when initializing spring boot project through IntelliJ IDEA.
---
- ***Folder structure / Packaging Structure*** 
  
	![](assets/Screenshot%202024-07-16%20112257.png)
	
	``` 
	│   .gitignore
	│   HELP.md //like readme.md
	│   mvnw
	│   mvnw.cmd //mevan command line
	│   pom.xml //like package.json in npm
	│
	├───.idea //specific for IntelliJ like .vscode in vs code
	│       .gitignore
	│       misc.xml
	│       vcs.xml
	│       workspace.xml
	│
	├───.mvn //for mevan configuration
	│   └───wrapper
	│           maven-wrapper.properties
	│
	└───src
			├───main
			│   ├───java //main java code
			│   │   └───com
			│   │       └───example
			│   │           └───demo
			│   │                   DemoApplication.java //Main java class
			│   │
			│   └───resources
			│       │   application.properties // DB configuration file
			│       │
			│       ├───static
			│       └───templates
			└───test //for java testing like JMeter
	```
- Automatically installed relevant packages using `Maven` built tool.
- Run the project using IntelliJ code runner. Then u can see few details on terminal window.
- `http://localhost:8080/` can see "Whitelabel Error Page" if server is running well

# Spring boot-PSR part 2

- Spring Boot Annotations
	- `@RestController` - using for REST API
	- `@Autowired` - dependency injection
	- `@Entity` - DB entities/table
	- `@Id` - Primary key
	- `@Query` - generating Query
	- `@RequestMapping` - generate base URL for API endpoint
	- `@GetMapping`,`@PostMapping`,`@PutMapping`,`@DeleteMapping` - Represent Get, Post, Put, Delete methods on REST APIs
	- `@CrossOrigin` - like CORS in express
	- `@Service` - for Java services, Interfaces
## Creating first REST API 
- Create new package/folder called `controller` inside `.com.example.demo` package
```
src
└───main
    └───java
        └───com
            └───example
                └───demo
                    └───controller
```
- Create `UserController` class inside the `controller` package.
- Inside the `UserController` class create simple get API end point
``` java 
package com.example.demo.controller;
//when annotation puts, automatically insert those import packages lines
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@CrossOrigin
//as a good patrice version is mentioned in base url
@RequestMapping(value="api/v1")
public class UserController {
    @GetMapping("/getUser")
    public String getUser() {
        return "Hello Usersad";
    }
}
```
![](assets/Pasted%20image%2020240716214740.png)
- Once a change sone need to stop and start server.

## Configure mysql db conection
- db configuration should be done in `application.properties` file which located at `src->main->resources`
``` bash
#application.properties
# in application.properties not using double quotation("") for the Strings & values
spring.application.name=demo

spring.jpa.hibernate.ddl-auto=update
# create a new database called "demodb" if it does not exist
spring.datasource.url=jdbc:mysql://localhost:3306/demodb?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.show-sql=true
```

# # Spring boot-PSR part 3
- Finalize packaging structure.
```
src 
└───main
    └───java
        └───com
            └───example
                └───demo
                    ├───controller
                    ├───dto //data transfer objct. iTelasoft
                    ├───model //sometimes called "entity"
                    ├───repo //contain Interfaces
                    └───service
``` 
- After that we create some java classes inside those
```
src
└───main
    └───java
        └───com
            └───example
                └───demo
                    │   DemoApplication.java
                    │
                    ├───controller
                    │       UserController.java
                    │
                    ├───dto
                    │       UserDTO.java
                    │
                    ├───model
                    │       User.java
                    │
                    ├───repo
                    │       UserRepo.java
                    │
                    └───service
                            UserService.java
```