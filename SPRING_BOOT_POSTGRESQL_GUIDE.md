# Beginner's Guide to Creating a Spring Boot REST API CRUD Application with PostgreSQL

This step-by-step guide will help you build a RESTful API using Spring Boot and PostgreSQL database from scratch. This guide is aimed at beginners with little to no experience with Spring Boot.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up Your Development Environment](#setting-up-your-development-environment)
3. [Creating a New Spring Boot Project](#creating-a-new-spring-boot-project)
4. [Configuring PostgreSQL Database](#configuring-postgresql-database)
5. [Creating the Project Structure](#creating-the-project-structure)
6. [Implementing the Model Layer](#implementing-the-model-layer)
7. [Creating the Repository Layer](#creating-the-repository-layer)
8. [Building the Service Layer](#building-the-service-layer)
9. [Implementing the Controller Layer](#implementing-the-controller-layer)
10. [Testing Your REST API](#testing-your-rest-api)
11. [Common Issues and Solutions](#common-issues-and-solutions)
12. [Next Steps](#next-steps)
13. [References](#references)

## Prerequisites

Before starting, make sure you have the following installed:

- JDK 17 or later (this guide uses JDK 17)
- IntelliJ IDEA (Community or Ultimate edition)
- PostgreSQL database server
- Basic understanding of Java programming

## Setting Up Your Development Environment

### Step 1: Install JDK 17

1. Download JDK 17 from [Oracle](https://www.oracle.com/java/technologies/downloads/#java17) or [OpenJDK](https://adoptium.net/)
2. Follow the installation instructions for your operating system
3. Verify installation by opening a terminal/command prompt and typing:
   ```
   java -version
   ```
   You should see output indicating Java 17

### Step 2: Install IntelliJ IDEA

1. Download IntelliJ IDEA from the [official website](https://www.jetbrains.com/idea/download/)
2. Choose Community Edition (free) or Ultimate Edition (paid, but has more features for Spring)
3. Follow the installation instructions for your operating system
4. Launch IntelliJ IDEA after installation

### Step 3: Install PostgreSQL

1. Download PostgreSQL from the [official website](https://www.postgresql.org/download/)
2. Follow the installation instructions for your operating system
3. During installation:
   - Note the port number (default is 5432)
   - Set a password for the 'postgres' user
   - Remember these credentials for later configuration

Alternatively, you can use Docker to run PostgreSQL:
```bash
docker run --name postgres-db -e POSTGRES_PASSWORD=your_password -d -p 5432:5432 postgres
```

## Creating a New Spring Boot Project

### Option 1: Using Spring Initializr in IntelliJ IDEA

1. Open IntelliJ IDEA
2. Click on "New Project"
3. Select "Spring Initializr" on the left panel
4. Configure your project:
   - **Name**: `spring-boot-postgresql-crud` (or your preferred name)
   - **Location**: Choose where to save your project
   - **Language**: Java
   - **Build System**: Maven
   - **JDK**: 17
   - **Java**: 17
   - **Packaging**: Jar
   - **Group**: `com.example` (or your preferred group ID)
   - **Artifact**: `crud-api` (or your preferred artifact ID)
5. Click "Next"
6. Add the following dependencies:
   - **Spring Web**: For building REST APIs
   - **Spring Data JPA**: For database access
   - **PostgreSQL Driver**: For connecting to PostgreSQL
   - **Validation**: For input validation
   - **Lombok** (optional): To reduce boilerplate code
7. Click "Create" to generate the project

### Option 2: Using Spring Initializr Web Interface

1. Visit [Spring Initializr](https://start.spring.io/)
2. Configure your project:
   - **Project**: Maven
   - **Language**: Java
   - **Spring Boot**: Select the latest stable version (e.g., 3.2.0)
   - **Group**: `com.example` (or your preferred group ID)
   - **Artifact**: `crud-api` (or your preferred artifact ID)
   - **Name**: `spring-boot-postgresql-crud` (or your preferred name)
   - **Description**: Add a description of your project
   - **Package name**: Auto-generated based on group and artifact
   - **Packaging**: Jar
   - **Java**: 17
3. Add the following dependencies:
   - **Spring Web**
   - **Spring Data JPA**
   - **PostgreSQL Driver**
   - **Validation**
   - **Lombok** (optional)
4. Click "Generate" to download the project as a ZIP file
5. Extract the ZIP file
6. Open IntelliJ IDEA
7. Select "Open" and navigate to the extracted project folder
8. Click "OK" to open the project

## Configuring PostgreSQL Database

### Step 1: Create a New Database

1. Open pgAdmin (comes with PostgreSQL installation) or use a terminal/command line
2. Log in to PostgreSQL with the credentials you set during installation
3. Create a new database named `crud_db`:

Using pgAdmin:
- Right-click on "Databases"
- Select "Create" → "Database"
- Enter `crud_db` as the name
- Click "Save"

Using command line:
```bash
psql -U postgres
CREATE DATABASE crud_db;
\q
```

### Step 2: Configure Database Connection in Spring Boot

1. Open `src/main/resources/application.properties` in IntelliJ
2. Add the following properties:

```properties
# PostgreSQL Database Configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/crud_db
spring.datasource.username=postgres
spring.datasource.password=your_password
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA/Hibernate Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# Server Configuration
server.port=8080
```

Replace `your_password` with your actual PostgreSQL password.

**Key Configuration Explanation:**
- `spring.jpa.hibernate.ddl-auto=update`: Automatically updates the database schema based on entity classes
- `spring.jpa.show-sql=true`: Shows SQL queries in the console for debugging
- `spring.jpa.properties.hibernate.dialect`: Specifies the PostgreSQL dialect for Hibernate

## Creating the Project Structure

For a well-organized CRUD application, create the following package structure:

1. Right-click on your base package (e.g., `com.example.crudapi`) in IntelliJ
2. Select "New" → "Package"
3. Create the following packages:
   - `model` (or `entity`): For entity classes mapped to database tables
   - `repository`: For database access interfaces
   - `service`: For business logic
   - `controller`: For REST API endpoints
   - `exception` (optional): For custom exceptions and error handling
   - `dto` (optional): For Data Transfer Objects

Your project structure should look like:
```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── example/
│   │           └── crudapi/
│   │               ├── CrudApiApplication.java
│   │               ├── controller/
│   │               ├── model/
│   │               ├── repository/
│   │               ├── service/
│   │               ├── exception/
│   │               └── dto/
│   └── resources/
│       └── application.properties
└── test/
    └── java/
        └── com/
            └── example/
                └── crudapi/
                    └── CrudApiApplicationTests.java
```

## Implementing the Model Layer

Let's create a simple `Product` entity as an example.

1. Right-click on the `model` package
2. Select "New" → "Java Class"
3. Name it `Product`
4. Add the following code:

```java
package com.example.crudapi.model;

import jakarta.persistence.*;
import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.NotNull;
import jakarta.validation.constraints.Positive;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.math.BigDecimal;

@Entity
@Table(name = "products")
@Data               // Lombok: generates getters, setters, toString, equals, hashCode
@NoArgsConstructor  // Lombok: generates a no-args constructor
@AllArgsConstructor // Lombok: generates an all-args constructor
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @NotBlank(message = "Name is required")
    private String name;

    private String description;

    @NotNull(message = "Price is required")
    @Positive(message = "Price must be positive")
    private BigDecimal price;

    @NotNull(message = "Quantity is required")
    @Positive(message = "Quantity must be positive")
    private Integer quantity;
}
```

**Note:** If you're not using Lombok, you'll need to manually add:
- Getters and setters for all fields
- Constructors (no-args and all-args)
- toString(), equals(), and hashCode() methods

## Creating the Repository Layer

1. Right-click on the `repository` package
2. Select "New" → "Java Class"
3. Name it `ProductRepository`
4. Create it as an interface and add the following code:

```java
package com.example.crudapi.repository;

import com.example.crudapi.model.Product;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    // Spring Data JPA automatically provides CRUD operations
    // Custom query methods can be added here if needed
}
```

The `JpaRepository` interface provides all basic CRUD operations:
- `save()`: Create or update an entity
- `findById()`: Find an entity by ID
- `findAll()`: Find all entities
- `deleteById()`: Delete an entity by ID
- And more...

## Building the Service Layer

1. Right-click on the `service` package
2. Select "New" → "Java Class"
3. Create an interface called `ProductService`:

```java
package com.example.crudapi.service;

import com.example.crudapi.model.Product;
import java.util.List;

public interface ProductService {
    List<Product> getAllProducts();
    Product getProductById(Long id);
    Product createProduct(Product product);
    Product updateProduct(Long id, Product productDetails);
    void deleteProduct(Long id);
}
```

4. Create the implementation class `ProductServiceImpl`:

```java
package com.example.crudapi.service;

import com.example.crudapi.model.Product;
import com.example.crudapi.repository.ProductRepository;
import jakarta.persistence.EntityNotFoundException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
public class ProductServiceImpl implements ProductService {

    private final ProductRepository productRepository;

    @Autowired
    public ProductServiceImpl(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    @Override
    public List<Product> getAllProducts() {
        return productRepository.findAll();
    }

    @Override
    public Product getProductById(Long id) {
        return productRepository.findById(id)
                .orElseThrow(() -> new EntityNotFoundException("Product not found with id: " + id));
    }

    @Override
    @Transactional
    public Product createProduct(Product product) {
        return productRepository.save(product);
    }

    @Override
    @Transactional
    public Product updateProduct(Long id, Product productDetails) {
        Product product = getProductById(id);
        
        product.setName(productDetails.getName());
        product.setDescription(productDetails.getDescription());
        product.setPrice(productDetails.getPrice());
        product.setQuantity(productDetails.getQuantity());
        
        return productRepository.save(product);
    }

    @Override
    @Transactional
    public void deleteProduct(Long id) {
        Product product = getProductById(id);
        productRepository.delete(product);
    }
}
```

## Implementing the Controller Layer

1. Right-click on the `controller` package
2. Select "New" → "Java Class"
3. Name it `ProductController`
4. Add the following code:

```java
package com.example.crudapi.controller;

import com.example.crudapi.model.Product;
import com.example.crudapi.service.ProductService;
import jakarta.validation.Valid;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/products")
public class ProductController {

    private final ProductService productService;

    @Autowired
    public ProductController(ProductService productService) {
        this.productService = productService;
    }

    // GET all products
    @GetMapping
    public ResponseEntity<List<Product>> getAllProducts() {
        List<Product> products = productService.getAllProducts();
        return new ResponseEntity<>(products, HttpStatus.OK);
    }

    // GET a product by ID
    @GetMapping("/{id}")
    public ResponseEntity<Product> getProductById(@PathVariable Long id) {
        Product product = productService.getProductById(id);
        return new ResponseEntity<>(product, HttpStatus.OK);
    }

    // CREATE a new product
    @PostMapping
    public ResponseEntity<Product> createProduct(@Valid @RequestBody Product product) {
        Product newProduct = productService.createProduct(product);
        return new ResponseEntity<>(newProduct, HttpStatus.CREATED);
    }

    // UPDATE a product
    @PutMapping("/{id}")
    public ResponseEntity<Product> updateProduct(@PathVariable Long id, 
                                               @Valid @RequestBody Product product) {
        Product updatedProduct = productService.updateProduct(id, product);
        return new ResponseEntity<>(updatedProduct, HttpStatus.OK);
    }

    // DELETE a product
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteProduct(@PathVariable Long id) {
        productService.deleteProduct(id);
        return new ResponseEntity<>(HttpStatus.NO_CONTENT);
    }
}
```

## Adding Exception Handling (Optional but Recommended)

1. Create a custom exception class in the `exception` package:

```java
package com.example.crudapi.exception;

public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

2. Create a global exception handler:

```java
package com.example.crudapi.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.context.request.WebRequest;

import jakarta.persistence.EntityNotFoundException;
import java.time.LocalDateTime;
import java.util.HashMap;
import java.util.Map;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorDetails> handleResourceNotFoundException(
            ResourceNotFoundException ex, WebRequest request) {
        
        ErrorDetails errorDetails = new ErrorDetails(
                LocalDateTime.now(),
                ex.getMessage(),
                request.getDescription(false));
        
        return new ResponseEntity<>(errorDetails, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(EntityNotFoundException.class)
    public ResponseEntity<ErrorDetails> handleEntityNotFoundException(
            EntityNotFoundException ex, WebRequest request) {
        
        ErrorDetails errorDetails = new ErrorDetails(
                LocalDateTime.now(),
                ex.getMessage(),
                request.getDescription(false));
        
        return new ResponseEntity<>(errorDetails, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Object> handleMethodArgumentNotValid(
            MethodArgumentNotValidException ex, WebRequest request) {
        
        Map<String, String> errors = new HashMap<>();
        
        ex.getBindingResult().getFieldErrors().forEach(error -> 
            errors.put(error.getField(), error.getDefaultMessage())
        );
        
        ValidationErrorResponse errorDetails = new ValidationErrorResponse(
                LocalDateTime.now(),
                "Validation Failed",
                request.getDescription(false),
                errors);
        
        return new ResponseEntity<>(errorDetails, HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorDetails> handleGlobalException(
            Exception ex, WebRequest request) {
        
        ErrorDetails errorDetails = new ErrorDetails(
                LocalDateTime.now(),
                ex.getMessage(),
                request.getDescription(false));
        
        return new ResponseEntity<>(errorDetails, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

3. Create error response classes:

```java
package com.example.crudapi.exception;

import java.time.LocalDateTime;

public class ErrorDetails {
    private LocalDateTime timestamp;
    private String message;
    private String details;

    public ErrorDetails(LocalDateTime timestamp, String message, String details) {
        this.timestamp = timestamp;
        this.message = message;
        this.details = details;
    }

    // Getters and setters
    public LocalDateTime getTimestamp() {
        return timestamp;
    }

    public void setTimestamp(LocalDateTime timestamp) {
        this.timestamp = timestamp;
    }

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public String getDetails() {
        return details;
    }

    public void setDetails(String details) {
        this.details = details;
    }
}
```

```java
package com.example.crudapi.exception;

import java.time.LocalDateTime;
import java.util.Map;

public class ValidationErrorResponse extends ErrorDetails {
    private Map<String, String> validationErrors;

    public ValidationErrorResponse(LocalDateTime timestamp, String message, 
                                  String details, Map<String, String> validationErrors) {
        super(timestamp, message, details);
        this.validationErrors = validationErrors;
    }

    public Map<String, String> getValidationErrors() {
        return validationErrors;
    }

    public void setValidationErrors(Map<String, String> validationErrors) {
        this.validationErrors = validationErrors;
    }
}
```

## Running the Application

1. In IntelliJ IDEA, locate the main application class (e.g., `CrudApiApplication.java`)
2. Right-click on the file and select "Run" or click the green play button in the margin

Alternatively, you can run it from the terminal:
```bash
./mvnw spring-boot:run
```

The application will start on port 8080 (or the port you configured).

## Testing Your REST API

You can test your API using various tools:

### Option 1: Using Postman

1. Download and install [Postman](https://www.postman.com/downloads/)
2. Create a new request:
   - **GET** `http://localhost:8080/api/products` to get all products
   - **GET** `http://localhost:8080/api/products/1` to get a product by ID
   - **POST** `http://localhost:8080/api/products` to create a product
     - Set the body to raw JSON:
     ```json
     {
       "name": "Laptop",
       "description": "High-performance laptop",
       "price": 1299.99,
       "quantity": 10
     }
     ```
   - **PUT** `http://localhost:8080/api/products/1` to update a product
     - Use similar JSON body as for POST
   - **DELETE** `http://localhost:8080/api/products/1` to delete a product

### Option 2: Using cURL

**Get all products:**
```bash
curl -X GET http://localhost:8080/api/products
```

**Get a product by ID:**
```bash
curl -X GET http://localhost:8080/api/products/1
```

**Create a new product:**
```bash
curl -X POST http://localhost:8080/api/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop","description":"High-performance laptop","price":1299.99,"quantity":10}'
```

**Update a product:**
```bash
curl -X PUT http://localhost:8080/api/products/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"Updated Laptop","description":"Updated description","price":1499.99,"quantity":15}'
```

**Delete a product:**
```bash
curl -X DELETE http://localhost:8080/api/products/1
```

### Option 3: Using IntelliJ HTTP Client (Ultimate Edition)

If you have IntelliJ IDEA Ultimate, you can create a file with `.http` extension and write:

```
### Get all products
GET http://localhost:8080/api/products

### Get a product by ID
GET http://localhost:8080/api/products/1

### Create a new product
POST http://localhost:8080/api/products
Content-Type: application/json

{
  "name": "Laptop",
  "description": "High-performance laptop",
  "price": 1299.99,
  "quantity": 10
}

### Update a product
PUT http://localhost:8080/api/products/1
Content-Type: application/json

{
  "name": "Updated Laptop",
  "description": "Updated description",
  "price": 1499.99,
  "quantity": 15
}

### Delete a product
DELETE http://localhost:8080/api/products/1
```

## Common Issues and Solutions

### 1. Database Connection Issues

**Problem**: Application fails to connect to PostgreSQL.

**Solutions**:
- Verify PostgreSQL is running (`sudo service postgresql status` on Linux)
- Check credentials in `application.properties`
- Ensure database exists
- Verify port number (default is 5432)

### 2. JPA/Hibernate Issues

**Problem**: Entity mapping issues.

**Solutions**:
- Check entity annotations (`@Entity`, `@Table`, etc.)
- Verify ID generation strategy
- Check field types match database column types
- Add `spring.jpa.properties.hibernate.show_sql=true` for debugging

### 3. Bean Creation Issues

**Problem**: Spring Boot fails to create beans.

**Solutions**:
- Ensure all required annotations are present (`@Service`, `@Repository`, etc.)
- Check for circular dependencies
- Verify package structure for component scanning

### 4. Validation Issues

**Problem**: Validation fails or doesn't work.

**Solutions**:
- Ensure `@Valid` annotation is added to controller methods
- Verify validation annotations on entity fields
- Check for proper exception handling

## Next Steps

After completing this basic CRUD application, you might want to explore:

1. **Authentication and Authorization**: Implement Spring Security
2. **API Documentation**: Add Swagger/OpenAPI with SpringDoc
3. **DTO Pattern**: Use DTOs to separate API models from database entities
4. **Pagination and Sorting**: Enhance your API with pagination
5. **Testing**: Write unit and integration tests
6. **Caching**: Implement caching for better performance
7. **Logging**: Add comprehensive logging
8. **Containerization**: Dockerize your application

## References

### Official Documentation

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [Spring Data JPA Documentation](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Hibernate Documentation](https://hibernate.org/orm/documentation/)
- [Jakarta Bean Validation Documentation](https://jakarta.ee/specifications/bean-validation/3.0/jakarta-bean-validation-spec-3.0.html)

### Tutorials and Guides

- [Spring Boot Guides](https://spring.io/guides)
- [Baeldung Spring Boot Tutorials](https://www.baeldung.com/spring-boot)
- [Spring Boot with PostgreSQL on Spring.io](https://spring.io/guides/gs/accessing-data-jpa/)
- [Building REST Services with Spring](https://spring.io/guides/tutorials/rest/)

### Additional Resources

- [Spring Framework API Documentation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/)
- [IntelliJ IDEA Documentation](https://www.jetbrains.com/help/idea/getting-started.html)
- [Maven Documentation](https://maven.apache.org/guides/index.html)
- [JPA Annotations Reference](https://www.objectdb.com/api/java/jpa/annotations)

---

This guide serves as a starting point for building Spring Boot REST APIs with PostgreSQL. As you become more familiar with Spring Boot, explore the references for deeper understanding and advanced features.
