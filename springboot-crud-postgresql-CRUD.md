# Spring Boot CRUD Application with PostgreSQL

A comprehensive, beginner-friendly Spring Boot CRUD (Create, Read, Update, Delete) application that demonstrates best practices for building REST APIs with PostgreSQL database integration using Docker.

## 📋 Table of Contents

- [Features](#-features)
- [Technologies Used](#-technologies-used)
- [Project Structure](#📁%20Project%20Structure)
- [Prerequisites](#-prerequisites)
- [Quick Start Guide](#-quick-start-guide)
- [Dependencies Explanation](#-dependencies-explanation)
- [Database Setup with Docker](#🐳%20Database%20Setup%20with%20Docker)
- [Running the Application](#-running-the-application)
- [API Documentation](#-api-documentation)
- [API Endpoints](#-api-endpoints)
- [Testing the API](#-testing-the-api)
- [Troubleshooting](#-troubleshooting)
- [Learning Resources](#-learning-resources)

## 🚀 Features

- **Complete CRUD Operations**: Create, Read, Update, and Delete users
- **PostgreSQL Integration**: Production-ready database with Docker setup
- **Input Validation**: Comprehensive validation with custom error messages
- **Exception Handling**: Global exception handling with meaningful error responses
- **API Documentation**: Interactive Swagger/OpenAPI documentation
- **Docker Support**: Containerized PostgreSQL database
- **Sample Data**: Automatic initialization with sample users
- **Search Functionality**: Search users by name, email, and other criteria
- **RESTful Design**: Following REST API best practices

## 🛠 Technologies Used

| Technology          | Purpose                   | Version  |
| ------------------- | ------------------------- | -------- |
| **Java**            | Programming Language      | 17+      |
| **Spring Boot**     | Application Framework     | 3.2.0    |
| **Spring Data JPA** | Data Access Layer         | Included |
| **PostgreSQL**      | Database                  | 15.4     |
| **Docker**          | Database Containerization | Latest   |
| **Maven**           | Build Tool                | 3.6+     |
| **Swagger/OpenAPI** | API Documentation         | 2.2.0    |

## 📁 Project Structure

```
springboot-crud-app/
├── .gitignore                             # Git ignore file
├── .vscode/                               # VS Code configuration
│   └── tasks.json                         # Build and run tasks
├── README.md                              # Complete documentation
├── api-tests.http                         # API testing examples
├── docker-compose.yml                     # Docker configuration for PostgreSQL
├── pom.xml                                # Maven dependencies and configuration
├── run.sh                                 # Startup script (executable)
├── src/
│   └── main/
│       ├── java/com/example/springbootcrudapp/
│       │   ├── SpringbootCrudAppApplication.java  # Main application class
│       │   ├── model/
│       │   │   └── User.java                      # Entity/Model class
│       │   ├── repository/
│       │   │   └── UserRepository.java            # Data access layer
│       │   ├── service/
│       │   │   └── UserService.java               # Business logic layer
│       │   ├── controller/
│       │   │   └── UserController.java            # REST API endpoints
│       │   ├── exception/
│       │   │   └── GlobalExceptionHandler.java    # Error handling
│       │   └── config/
│       │       ├── OpenApiConfig.java             # Swagger configuration
│       │       └── DataInitializer.java           # Sample data setup
│       └── resources/
│           └── application.properties             # Application configuration
└── target/                                        # Compiled files (auto-generated)
```

## 📋 Prerequisites

Before running this application, ensure you have the following installed:

1. **Java Development Kit (JDK) 17 or higher**
   ```bash
   java -version
   ```

2. **Maven 3.6 or higher**
   ```bash
   mvn -version
   ```

3. **Docker and Docker Compose**
   ```bash
   docker --version
   docker-compose --version
   ```

4. **Git** (for cloning the repository)
   ```bash
   git --version
   ```

## 🚀 Quick Start Guide

### Step 1: Clone the Repository

```bash
# Clone the repository
git clone <your-repository-url>
cd Spring-boot

# Or if you're starting from scratch, navigate to your project directory
cd /home/rumindu/work-space-oxo/Spring-boot
```

### Step 2: Start PostgreSQL Database

```bash
# 1st and 2nd command need if there is no docker-compose
# Update package list
sudo apt update

# Install Docker Compose V2 as a plugin
sudo apt install docker-compose-plugin -y

# Start PostgreSQL using Docker Compose
docker compose up -d

# Verify containers are running
docker compose ps

```

Expected output:
```
NAME                     IMAGE                 COMMAND                  SERVICE    STATUS
springboot_pgadmin       dpage/pgadmin4:7.8    "/entrypoint.sh"         pgadmin    Up
springboot_postgres      postgres:15.4-alpine  "docker-entrypoint.s…"   postgres   Up
```

### Step 3: Install Dependencies

```bash
# Install Maven dependencies
mvn clean install
```

### Step 4: Run the Application

```bash
# Run the Spring Boot application
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

### Step 5: Access the Application

- **API Base URL**: http://localhost:8080/api/users
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **API Documentation**: http://localhost:8080/api-docs
- **pgAdmin** (Database Management): http://localhost:5050

## 📦 Dependencies Explanation

Our `pom.xml` includes several key dependencies. Here's why each one is important:

### Core Spring Boot Dependencies

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
**Why we need it**: Provides web capabilities including embedded Tomcat server, Spring MVC, and REST API support. Essential for creating web applications and REST services.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```
**Why we need it**: Provides JPA (Java Persistence API) and Hibernate ORM support. Simplifies database operations with automatic repository implementations and entity management.

### Database Dependencies

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```
**Why we need it**: PostgreSQL JDBC driver that enables the application to connect to PostgreSQL database. Required for database connectivity.

### Validation Dependencies

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
**Why we need it**: Provides validation annotations (@NotBlank, @Email, @Size) and automatic validation of request data. Ensures data integrity and provides meaningful error messages.

### Documentation Dependencies

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.2.0</version>
</dependency>
```
**Why we need it**: Automatically generates interactive API documentation (Swagger UI) from your code annotations. Essential for API documentation and testing.

### Development Dependencies

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
```
**Why we need it**: Provides development-time features like automatic application restart when code changes, improved development experience.

## 🐳 Database Setup with Docker

### Understanding docker-compose.yml

Our Docker Compose file sets up two services:

1. **PostgreSQL Database**:
   - Image: `postgres:15.4-alpine` (lightweight version)
   - Port: `5432` (standard PostgreSQL port)
   - Database: `springboot_crud_db`
   - Username: `springboot_user`
   - Password: `springboot_password`

2. **pgAdmin** (Optional Database Management UI):
   - Image: `dpage/pgadmin4:7.8`
   - Port: `5050`
   - Email: `admin@admin.com`
   - Password: `admin`

### Docker Commands

```bash
# Start all services
docker compose up -d

# View running containers
docker compose ps

# View logs
docker compose logs postgres
docker compose logs pgadmin

# Stop all services
docker compose down

# Stop and remove all volumes (deletes data)
docker compose down -v

# Restart services
docker compose restart
```

### Connecting to Database via pgAdmin

1. Open http://localhost:5050
2. Login with:
   - Email: `admin@admin.com`
   - Password: `admin`
3. Add server connection:
   - Host: `springboot_postgres` (service name)
   - Port: `5432`
   - Database: `springboot_crud_db`
   - Username: `springboot_user`
   - Password: `springboot_password`

## 🏃‍♂️ Running the Application

### Method 1: Using Maven

#### Quick Start (Recommended)
```bash
# Clean, compile, and run in one step
mvn clean spring-boot:run
```

#### Step-by-Step Approach
```bash
# Step 1: Clean previous builds and compile source code
mvn clean compile

# Step 2: Run the application
mvn spring-boot:run
```

#### Complete Build Process
```bash
# Clean, compile, test, and package (creates JAR file)
mvn clean install

# Then run the application
mvn spring-boot:run
```

#### Maven Command Explanation

| Command | Purpose | Output |
|---------|---------|--------|
| `mvn clean` | Deletes `target/` directory | Removes old build artifacts |
| `mvn compile` | Compiles main source code | Creates `.class` files in `target/classes/` |
| `mvn test` | Runs unit tests | Executes tests and generates reports |
| `mvn package` | Creates JAR/WAR file | Produces `target/*.jar` file |
| `mvn install` | All above + installs to local repo | Makes artifact available for other projects |
| `mvn spring-boot:run` | Runs Spring Boot application | Starts embedded Tomcat server |

#### Development Workflow Commands
```bash
# Quick compilation check (fastest)
mvn clean compile

# Full build with tests
mvn clean install

# Run without rebuilding (if already compiled)
mvn spring-boot:run

# Run with specific profile
mvn spring-boot:run -Dspring-boot.run.profiles=dev

# Run with JVM arguments
mvn spring-boot:run -Dspring-boot.run.jvmArguments="-Xmx512m"

# Run on different port
mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8081
```

#### Troubleshooting Maven Issues
```bash
# Force update dependencies
mvn clean install -U

# Skip tests if they're failing
mvn clean install -DskipTests

# Run with verbose output for debugging
mvn clean compile -X

# Check dependency tree
mvn dependency:tree
```

### Method 2: Using JAR file

```bash
# Build JAR file
mvn clean package

# Run the JAR file
java -jar target/springboot-crud-app-0.0.1-SNAPSHOT.jar
```

### Verify Application is Running

Look for these startup messages:
```
🚀 Spring Boot CRUD Application started successfully!
📝 Swagger UI: http://localhost:8080/swagger-ui.html
🔧 API Docs: http://localhost:8080/api-docs
```

## 🌱 Automatic Data Seeding

This application includes **automatic data initialization** that runs when the application starts. You'll see sample data in your database without manually inserting it.

### How It Works

The application uses a `DataInitializer` component that automatically seeds the database with sample users when the application starts:

**File**: `src/main/java/com/example/springbootcrudapp/config/DataInitializer.java`

```java
@Component
public class DataInitializer implements CommandLineRunner {
    
    @Autowired
    private UserRepository userRepository;

    @Override
    public void run(String... args) {
        // Only seed data if database is empty
        if (userRepository.count() == 0) {
            System.out.println("🌱 Initializing database with sample data...");
            
            // Creates 5 sample users with predefined data
            User user1 = new User("John", "Doe", "john.doe@example.com", 
                                "+1-555-0101", "123 Main St, New York, NY 10001");
            User user2 = new User("Jane", "Smith", "jane.smith@example.com", 
                                "+1-555-0102", "456 Oak Ave, Los Angeles, CA 90210");
            // ... 3 more users
            
            userRepository.save(user1);
            userRepository.save(user2);
            // ... saves all users
            
            System.out.println("✅ Sample data initialized successfully!");
        }
    }
}
```

### What Gets Created

When you start the application, **5 sample users** are automatically created:

1. **John Doe** - john.doe@example.com
2. **Jane Smith** - jane.smith@example.com  
3. **Bob Johnson** - bob.johnson@example.com
4. **Alice Brown** - alice.brown@example.com
5. **Charlie Wilson** - charlie.wilson@example.com

### Startup Messages

Watch for these messages in your console when the application starts:
```
🌱 Initializing database with sample data...
✅ Sample data initialized successfully!
📊 Total users created: 5
```

### Key Features

- **Conditional Seeding**: Only runs if the database is empty (`userRepository.count() == 0`)
- **Automatic Execution**: Runs automatically after Spring Boot startup
- **Development Friendly**: Provides immediate data for testing APIs
- **Production Safe**: Won't overwrite existing data

### Disable Data Seeding

If you don't want automatic data seeding, you can:

1. **Remove the component annotation**:
   ```java
   // @Component  // Comment out or remove this line
   public class DataInitializer implements CommandLineRunner {
   ```

2. **Delete the DataInitializer.java file** entirely

3. **Add conditional logic** for different environments:
   ```java
   @Profile("!production")  // Only run in non-production environments
   @Component
   public class DataInitializer implements CommandLineRunner {
   ```

### Verify Sample Data

After starting the application, verify the sample data was created:

```bash
# Using curl
curl http://localhost:8080/api/users

# Using pgAdmin (http://localhost:5050)
# Connect to database and run:
SELECT * FROM users;
```

## 📚 API Documentation

### Swagger UI Access

Visit http://localhost:8080/swagger-ui.html to access the interactive API documentation where you can:

- View all available endpoints
- Test API endpoints directly from the browser
- See request/response schemas
- Download API specification

### API Documentation JSON

Raw OpenAPI specification available at: http://localhost:8080/api-docs

## 🔗 API Endpoints

| Method   | Endpoint                        | Description          | Request Body |
| -------- | ------------------------------- | -------------------- | ------------ |
| `GET`    | `/api/users`                    | Get all users        | None         |
| `GET`    | `/api/users/{id}`               | Get user by ID       | None         |
| `GET`    | `/api/users/email/{email}`      | Get user by email    | None         |
| `POST`   | `/api/users`                    | Create new user      | User JSON    |
| `PUT`    | `/api/users/{id}`               | Update user          | User JSON    |
| `DELETE` | `/api/users/{id}`               | Delete user          | None         |
| `GET`    | `/api/users/search?name={name}` | Search users by name | None         |
| `GET`    | `/api/users/count`              | Get total user count | None         |
| `GET`    | `/api/users/exists/{id}`        | Check if user exists | None         |

### Sample User JSON

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phone": "+1-555-0101",
  "address": "123 Main St, New York, NY 10001"
}
```

## 🧪 Testing the API

### Using curl Commands

```bash
# Get all users
curl -X GET http://localhost:8080/api/users

# Get user by ID
curl -X GET http://localhost:8080/api/users/1

# Create new user
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "Test",
    "lastName": "User",
    "email": "test@example.com",
    "phone": "+1-555-0199",
    "address": "Test Address"
  }'

# Update user
curl -X PUT http://localhost:8080/api/users/1 \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "Updated",
    "lastName": "User",
    "email": "updated@example.com",
    "phone": "+1-555-0199",
    "address": "Updated Address"
  }'

# Delete user
curl -X DELETE http://localhost:8080/api/users/1

# Search users
curl -X GET "http://localhost:8080/api/users/search?name=John"
```

### Using Postman

1. Import the OpenAPI specification from http://localhost:8080/api-docs
2. Or manually create requests using the endpoints above
3. Set `Content-Type: application/json` for POST/PUT requests

## 🔧 Troubleshooting

### Common Issues and Solutions

#### 1. Database Connection Issues

**Problem**: `Connection refused` or `Database connection failed`

**Solutions**:
```bash
# Check if PostgreSQL container is running
docker-compose ps

# If not running, start it
docker-compose up -d postgres

# Check container logs
docker-compose logs postgres

# Verify port is not in use
netstat -tulpn | grep 5432
```

#### 2. Port Already in Use

**Problem**: `Port 8080 is already in use`

**Solutions**:
```bash
# Option 1: Kill process using port 8080
sudo lsof -t -i:8080 | xargs kill -9

# Option 2: Change port in application.properties
server.port=8081
```

#### 3. Maven Build Issues

**Problem**: Maven dependencies not downloading

**Solutions**:
```bash
# Clean Maven cache
mvn clean

# Force update dependencies
mvn clean install -U

# Check Java version
java -version  # Should be 17+
```

#### 4. Docker Issues

**Problem**: Docker containers not starting

**Solutions**:
```bash
# Remove existing containers and volumes
docker-compose down -v

# Rebuild and start
docker-compose up -d --force-recreate

# Check Docker daemon
sudo systemctl status docker
```

### Checking Application Health

```bash
# Check if application is running
curl http://localhost:8080/api/users/count

# Check database connectivity
docker-compose exec postgres psql -U springboot_user -d springboot_crud_db -c "SELECT version();"
```

## 📖 Learning Resources

### Spring Boot Concepts

1. **MVC Architecture**: 
   - Model: `User.java` (Entity)
   - View: REST API responses (JSON)
   - Controller: `UserController.java`

2. **Dependency Injection**: 
   - `@Autowired` annotations in Service and Controller classes

3. **JPA/Hibernate**:
   - Entity mapping with `@Entity`
   - Repository pattern with `JpaRepository`
   - Automatic table creation with `ddl-auto=update`

4. **Validation**:
   - Bean validation with `@NotBlank`, `@Email`, `@Size`
   - Global exception handling

### 🎯 Next Steps for Learning

1. **Add Security**: Implement Spring Security for authentication
2. **Add Testing**: Write unit and integration tests
3. **Add Caching**: Implement Redis caching
4. **Add Logging**: Configure proper logging with Logback
5. **Add Profiles**: Separate configurations for dev/prod environments
6. Add API versioning
7. Implement pagination for large datasets

### Useful Spring Boot Links

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Spring Data JPA Reference](https://spring.io/projects/spring-data-jpa)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)

---

## 📝 Spring Boot Annotations Explained

This project uses various Spring Boot annotations that are fundamental to understanding how the framework works. Here's a detailed explanation of each annotation used and why it's important:

### 🏗️ Core Spring Boot Annotations

#### `@SpringBootApplication`
**File**: `SpringbootCrudAppApplication.java`
```java
@SpringBootApplication
public class SpringbootCrudAppApplication {
    // Main application class
}
```
**What it does**: This is a meta-annotation that combines three important annotations:
- `@Configuration`: Marks the class as a source of bean definitions
- `@EnableAutoConfiguration`: Enables Spring Boot's auto-configuration mechanism
- `@ComponentScan`: Enables component scanning for the current package and sub-packages

**Why we use it**: It's the entry point of our Spring Boot application and automatically configures many things we need.

---

### 🗂️ Entity and Data Annotations

#### `@Entity`
**File**: `User.java`
```java
@Entity
@Table(name = "users")
public class User {
    // Entity class
}
```
**What it does**: Marks this class as a JPA entity that represents a table in the database.

**Why we use it**: Tells Spring Data JPA that this class should be mapped to a database table.

#### `@Table(name = "users")`
**What it does**: Specifies the name of the database table this entity maps to.

**Why we use it**: Without this, JPA would use the class name as the table name. We explicitly name it "users" for clarity.

#### `@Id`
```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
**What it does**: Marks this field as the primary key of the entity.

**Why we use it**: Every JPA entity must have a primary key to uniquely identify records.

#### `@GeneratedValue(strategy = GenerationType.IDENTITY)`
**What it does**: Tells JPA to auto-generate the primary key value using the database's identity column.

**Why we use it**: We want the database to automatically assign unique IDs to new users.

#### `@Column`
```java
@Column(name = "first_name", nullable = false)
private String firstName;
```
**What it does**: Maps the field to a specific database column with additional constraints.

**Why we use it**: Allows us to specify column names, constraints, and properties that differ from the field name.

#### `@CreationTimestamp` and `@UpdateTimestamp`
```java
@CreationTimestamp
@Column(name = "created_at", updatable = false)
private LocalDateTime createdAt;

@UpdateTimestamp
@Column(name = "updated_at")
private LocalDateTime updatedAt;
```
**What they do**: Automatically set timestamps when records are created or updated.

**Why we use them**: Provides automatic audit trails without writing custom code.

---

### ✅ Validation Annotations

#### `@NotBlank`
```java
@NotBlank(message = "First name is required")
private String firstName;
```
**What it does**: Ensures the field is not null, empty, or contains only whitespace.

**Why we use it**: Validates that required fields have meaningful content.

#### `@Size`
```java
@Size(min = 2, max = 50, message = "First name must be between 2 and 50 characters")
private String firstName;
```
**What it does**: Validates that the field length is within specified bounds.

**Why we use it**: Ensures data fits database constraints and meets business rules.

#### `@Email`
```java
@Email(message = "Email should be valid")
private String email;
```
**What it does**: Validates that the field contains a properly formatted email address.

**Why we use it**: Ensures email data integrity and prevents invalid email addresses.

---

### 🗃️ Repository Annotations

#### `@Repository`
**File**: `UserRepository.java`
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    // Repository methods
}
```
**What it does**: Marks the interface as a Spring Data repository component.

**Why we use it**: Enables Spring to automatically implement CRUD operations and custom query methods.

#### `@Query`
```java
@Query("SELECT u FROM User u WHERE LOWER(u.firstName) LIKE LOWER(CONCAT('%', :name, '%'))")
List<User> findByNameContaining(@Param("name") String name);
```
**What it does**: Allows you to define custom JPQL or SQL queries.

**Why we use it**: When method name conventions aren't sufficient for complex queries.

#### `@Param`
**What it does**: Binds method parameters to query parameters.

**Why we use it**: Safely passes parameters to custom queries, preventing SQL injection.

---

### 🔧 Service Layer Annotations

#### `@Service`
**File**: `UserService.java`
```java
@Service
public class UserService {
    // Business logic
}
```
**What it does**: Marks the class as a Spring service component containing business logic.

**Why we use it**: Makes the class eligible for dependency injection and clearly identifies it as a service layer component.

#### `@Autowired`
```java
@Autowired
private UserRepository userRepository;
```
**What it does**: Automatically injects dependencies into the class.

**Why we use it**: Implements dependency injection, allowing Spring to provide required dependencies automatically.

---

### 🌐 Controller Annotations

#### `@RestController`
**File**: `UserController.java`
```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    // REST endpoints
}
```
**What it does**: Combines `@Controller` and `@ResponseBody`, indicating this class handles REST requests and returns JSON responses.

**Why we use it**: Creates RESTful web services that return data instead of views.

#### `@RequestMapping("/api/users")`
**What it does**: Maps HTTP requests to handler methods and sets the base URL path.

**Why we use it**: Defines the URL structure for all endpoints in this controller.

#### `@CrossOrigin(origins = "*")`
**What it does**: Enables Cross-Origin Resource Sharing (CORS) for frontend integration.

**Why we use it**: Allows web browsers to make requests from different domains (needed for frontend apps).

#### HTTP Method Annotations

```java
@GetMapping("/{id}")
public ResponseEntity<User> getUserById(@PathVariable Long id) {
    // GET method implementation
}

@PostMapping
public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
    // POST method implementation
}

@PutMapping("/{id}")
public ResponseEntity<User> updateUser(@PathVariable Long id, @Valid @RequestBody User user) {
    // PUT method implementation
}

@DeleteMapping("/{id}")
public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
    // DELETE method implementation
}
```

#### `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`
**What they do**: Shorthand annotations for mapping specific HTTP methods to handler methods.

**Why we use them**: More concise than `@RequestMapping(method = RequestMethod.GET)` and clearly shows the HTTP method.

#### `@PathVariable`
```java
@GetMapping("/{id}")
public ResponseEntity<User> getUserById(@PathVariable Long id) {
    // Method implementation
}
```
**What it does**: Extracts values from the URL path and binds them to method parameters.

**Why we use it**: Allows us to capture dynamic parts of the URL (like user IDs).

#### `@RequestBody`
```java
@PostMapping
public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
    // Method implementation
}
```
**What it does**: Binds the HTTP request body to a Java object.

**Why we use it**: Converts JSON from the request body into User objects automatically.

#### `@Valid`
```java
public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
    // Method implementation
}
```
**What it does**: Triggers validation of the request body using Bean Validation annotations.

**Why we use it**: Automatically validates input data before processing, ensuring data integrity.

#### `@RequestParam`
```java
@GetMapping("/search")
public ResponseEntity<List<User>> searchUsers(@RequestParam String name) {
    // Method implementation
}
```
**What it does**: Binds HTTP request parameters to method parameters.

**Why we use it**: Captures query parameters from URLs like `/search?name=John`.

---

### 🚨 Exception Handling Annotations

#### `@RestControllerAdvice`
**File**: `GlobalExceptionHandler.java`
```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    // Exception handling methods
}
```
**What it does**: Makes this class handle exceptions globally across all controllers.

**Why we use it**: Provides centralized exception handling and consistent error responses.

#### `@ExceptionHandler`
```java
@ExceptionHandler(MethodArgumentNotValidException.class)
public ResponseEntity<Map<String, Object>> handleValidationExceptions(
        MethodArgumentNotValidException ex) {
    // Exception handling logic
}
```
**What it does**: Specifies which exception types this method should handle.

**Why we use it**: Provides custom handling for specific exception types with meaningful error messages.

---

### ⚙️ Configuration Annotations

#### `@Configuration`
**File**: `OpenApiConfig.java`
```java
@Configuration
public class OpenApiConfig {
    // Configuration beans
}
```
**What it does**: Marks the class as a source of bean definitions for the application context.

**Why we use it**: Allows us to define custom configuration beans (like Swagger setup).

#### `@Bean`
```java
@Bean
public OpenAPI userManagementOpenAPI() {
    return new OpenAPI()
        .info(new Info()
            .title("Spring Boot CRUD API"));
}
```
**What it does**: Indicates that the method produces a bean to be managed by the Spring container.

**Why we use it**: Creates and configures the OpenAPI documentation object.

#### `@Component`
**File**: `DataInitializer.java`
```java
@Component
public class DataInitializer implements CommandLineRunner {
    // Initialization logic
}
```
**What it does**: Marks the class as a Spring component for automatic detection and registration.

**Why we use it**: Makes the class eligible for dependency injection and automatic execution.

---

### 📚 Swagger/OpenAPI Annotations

#### `@Tag`
```java
@Tag(name = "User Management", description = "APIs for managing users")
```
**What it does**: Groups related API endpoints together in the Swagger documentation.

**Why we use it**: Organizes API documentation for better readability.

#### `@Operation`
```java
@Operation(summary = "Get all users", description = "Retrieve a list of all users")
```
**What it does**: Provides detailed documentation for individual API endpoints.

**Why we use it**: Makes API documentation more informative and user-friendly.

#### `@ApiResponse` and `@ApiResponses`
```java
@ApiResponses(value = {
    @ApiResponse(responseCode = "200", description = "User found"),
    @ApiResponse(responseCode = "404", description = "User not found")
})
```
**What they do**: Document possible HTTP response codes and their meanings.

**Why we use them**: Help API consumers understand what responses to expect.

#### `@Parameter`
```java
@Parameter(description = "User ID", required = true) @PathVariable Long id
```
**What it does**: Documents method parameters in the API specification.

**Why we use it**: Provides clear documentation about what parameters are expected.

---

### 🎯 Key Benefits of Using Annotations

1. **Declarative Programming**: Annotations tell Spring what to do without writing boilerplate code
2. **Automatic Configuration**: Spring automatically configures beans and dependencies
3. **Clean Code**: Reduces the amount of XML configuration and repetitive code
4. **Type Safety**: Compile-time checking for many configurations
5. **Documentation**: Many annotations serve as both configuration and documentation
6. **Consistency**: Standard patterns across all Spring applications

Understanding these annotations is crucial for Spring Boot development as they form the foundation of how the framework operates and automates many common tasks.

---
