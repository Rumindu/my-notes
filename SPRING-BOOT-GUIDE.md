# 📚 Complete Spring Boot Learning Guide & Microservices Migration

A comprehensive guide covering Spring Boot annotations, dependencies, and step-by-step microservices conversion with practical examples and references.

## 📋 Table of Contents

- [Spring Boot Annotations Reference](#-spring-boot-annotations-reference)
- [Official Documentation Links](#-official-documentation-links)
- [Complete Annotation Categories](#-complete-annotation-categories)
- [Converting to Microservices](#-converting-to-microservices-architecture)
- [Dependencies for Microservices](#-dependencies-for-microservices)
- [Step-by-Step Migration Guide](#-step-by-step-microservices-conversion)
- [Docker Configuration](#-docker-compose-for-microservices)
- [Essential References](#-essential-microservices-references)
- [Best Practices](#-best-practices-and-patterns)

---

## 📚 Spring Boot Annotations Reference

### Official Documentation Links

| Resource | URL | Description |
|----------|-----|-------------|
| **Spring Boot Reference** | https://docs.spring.io/spring-boot/docs/current/reference/html/ | Complete Spring Boot documentation |
| **Spring Framework Annotations** | https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-annotation-config | Core Spring annotations |
| **Spring Data JPA** | https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#reference | JPA and database annotations |
| **Spring Web MVC** | https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann | Web and REST annotations |
| **Spring Security** | https://docs.spring.io/spring-security/reference/ | Security annotations |
| **Spring Cloud** | https://docs.spring.io/spring-cloud/docs/current/reference/html/ | Microservices annotations |

---

## 🏷️ Complete Annotation Categories

### 🏗️ Core Spring Boot Annotations

```java
// Application Entry Point
@SpringBootApplication  // Combines @Configuration, @EnableAutoConfiguration, @ComponentScan
public class Application { }

// Component Stereotypes
@Component              // Generic Spring component
@Service               // Service layer component
@Repository            // Data access layer component
@Controller            // Web MVC controller
@RestController        // REST API controller (combines @Controller + @ResponseBody)
@Configuration         // Configuration class
@Bean                  // Bean definition method

// Component Scanning & Auto-Configuration
@ComponentScan         // Define component scanning packages
@EnableAutoConfiguration // Enable Spring Boot auto-configuration
@ConditionalOnProperty // Conditional bean creation based on properties
@ConditionalOnClass    // Conditional bean creation based on class presence
```

### 🌐 Web & REST API Annotations

```java
// Request Mapping
@RequestMapping(value = "/api", method = RequestMethod.GET)
@GetMapping("/users")      // GET requests
@PostMapping("/users")     // POST requests
@PutMapping("/users/{id}") // PUT requests
@DeleteMapping("/users/{id}") // DELETE requests
@PatchMapping("/users/{id}")  // PATCH requests

// Request Parameters
@PathVariable("id")        // Extract path variables: /users/{id}
@RequestParam("name")      // Extract query parameters: ?name=value
@RequestBody              // Map request body to object
@RequestHeader("Authorization") // Extract HTTP headers
@CookieValue("sessionId") // Extract cookie values

// Response Handling
@ResponseBody             // Return response as JSON/XML
@ResponseStatus(HttpStatus.CREATED) // Set HTTP status code
@CrossOrigin              // Enable CORS support
@Valid                    // Enable request validation

// Exception Handling
@ExceptionHandler         // Handle specific exceptions
@ControllerAdvice         // Global exception handling
@RestControllerAdvice     // REST-specific global exception handling
```

### 🗂️ Data & JPA Annotations

```java
// Entity Mapping
@Entity                   // JPA entity
@Table(name = "users")    // Database table mapping
@Id                       // Primary key
@GeneratedValue(strategy = GenerationType.IDENTITY) // Auto-generate values
@Column(name = "first_name", nullable = false) // Column mapping
@Transient               // Exclude field from persistence

// Relationships
@OneToOne                // One-to-one relationship
@OneToMany(mappedBy = "user", cascade = CascadeType.ALL) // One-to-many
@ManyToOne               // Many-to-one relationship
@ManyToMany              // Many-to-many relationship
@JoinColumn(name = "user_id") // Foreign key column
@JoinTable               // Join table for many-to-many

// Auditing
@CreationTimestamp       // Automatic creation timestamp
@UpdateTimestamp         // Automatic update timestamp
@CreatedDate             // Creation date (Spring Data)
@LastModifiedDate        // Last modified date (Spring Data)
@CreatedBy               // Created by user
@LastModifiedBy          // Last modified by user

// Repository
@Repository              // Data access component
@Query("SELECT u FROM User u WHERE u.email = ?1") // Custom JPQL query
@Modifying               // Modifying query (UPDATE/DELETE)
@Transactional           // Transaction management
```

### ✅ Validation Annotations

```java
// Basic Validation
@Valid                   // Enable validation
@NotNull                 // Field cannot be null
@NotEmpty                // Collection/array cannot be empty
@NotBlank                // String cannot be null, empty, or whitespace
@Size(min = 2, max = 50) // Size constraints
@Min(18)                 // Minimum numeric value
@Max(100)                // Maximum numeric value

// String Validation
@Email                   // Valid email format
@Pattern(regexp = "^[A-Z]{2}[0-9]{6}$") // Regex pattern
@Length(min = 8, max = 255) // String length (Hibernate)

// Date/Time Validation
@Past                    // Date must be in the past
@Future                  // Date must be in the future
@PastOrPresent          // Date must be past or present
@FutureOrPresent        // Date must be future or present

// Custom Validation
@AssertTrue             // Boolean field must be true
@AssertFalse            // Boolean field must be false
@Digits(integer = 3, fraction = 2) // Numeric format validation
```

### 🔧 Configuration & Properties Annotations

```java
// Configuration
@Configuration           // Configuration class
@PropertySource("classpath:app.properties") // Load properties file
@ConfigurationProperties(prefix = "app") // Bind properties to object
@Value("${app.name}")    // Inject property value
@Profile("dev")          // Profile-specific configuration
@Conditional(OnDatabaseCondition.class) // Conditional configuration

// Enable Features
@EnableJpaRepositories   // Enable JPA repositories
@EnableTransactionManagement // Enable transaction management
@EnableCaching           // Enable caching support
@EnableAsync             // Enable async processing
@EnableScheduling        // Enable scheduled tasks
@EnableWebSecurity       // Enable Spring Security
```

### 🔐 Security Annotations

```java
// Method Security
@Secured("ROLE_ADMIN")   // Role-based access
@PreAuthorize("hasRole('ADMIN')") // Expression-based security
@PostAuthorize("returnObject.owner == authentication.name") // Post-processing security
@RolesAllowed({"ADMIN", "USER"}) // JSR-250 annotation

// Class-level Security
@EnableGlobalMethodSecurity(prePostEnabled = true) // Enable method security
@EnableWebSecurity       // Enable web security configuration
```

### ⏰ Scheduling & Async Annotations

```java
// Scheduling
@Scheduled(fixedRate = 5000) // Execute every 5 seconds
@Scheduled(cron = "0 0 * * * *") // Cron expression
@EnableScheduling        // Enable scheduling support

// Async Processing  
@Async                   // Asynchronous method execution
@EnableAsync            // Enable async support
```

### 🧪 Testing Annotations

```java
// Spring Boot Testing
@SpringBootTest          // Integration test
@WebMvcTest(UserController.class) // Web layer test
@DataJpaTest            // JPA repository test
@JsonTest               // JSON serialization test
@TestConfiguration      // Test-specific configuration

// JUnit & Mockito
@Test                   // Test method
@MockBean               // Mock Spring bean
@SpyBean                // Spy on Spring bean
@TestPropertySource     // Override properties for tests
@ActiveProfiles("test") // Activate test profile
```

---

## 🚀 Converting to Microservices Architecture

### Current vs Microservices Architecture

### 🏗️ Current Monolithic Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                    🏢 MONOLITHIC APPLICATION                         │
│                         (Single JAR File)                            │
├──────────────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │                    📱 APPLICATION LAYERS                        │ │
│  │                                                                 │ │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  │ │
│  │  │   👤 User       │  │   🛒 Order      │  │   💳 Payment    │  │ │
│  │  │   Management    │  │   Processing    │  │   Handling      │  │ │
│  │  │   Controllers   │  │   Controllers   │  │   Controllers   │  │ │
│  │  └─────────────────┘  └─────────────────┘  └─────────────────┘  │ │
│  │                                                                 │ │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  │ │
│  │  │   👤 User       │  │   🛒 Order      │  │   💳 Payment    │  │ │
│  │  │   Services      │  │   Services      │  │   Services      │  │ │
│  │  └─────────────────┘  └─────────────────┘  └─────────────────┘  │ │
│  │                                                                 │ │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  │ │
│  │  │   👤 User       │  │   🛒 Order      │  │   💳 Payment    │  │ │
│  │  │   Repositories  │  │   Repositories  │  │   Repositories  │  │ │
│  │  └─────────────────┘  └─────────────────┘  └─────────────────┘  │ │
│  └─────────────────────────────────────────────────────────────────┘ │
├──────────────────────────────────────────────────────────────────────┤
│  🗄️  SINGLE SHARED DATABASE (PostgreSQL)                             │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐       │
│  │   users table   │  │   orders table  │  │  payments table │       │
│  │   addresses     │  │   order_items   │  │  transactions   │       │
│  │   profiles      │  │   inventory     │  │  receipts       │       │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘       │
└──────────────────────────────────────────────────────────────────────┘

Problems: ❌ Single point of failure  ❌ Difficult to scale  
          ❌ Technology lock-in       ❌ Large deployment size
          ❌ Team dependencies        ❌ Complex testing
```

### 🚀 Target Microservices Architecture

```
                              ☁️  MICROSERVICES ECOSYSTEM
┌───────────────────────────────────────────────────────────────────────┐
│                                                                       │
│  🌐 INFRASTRUCTURE LAYER                                              │
│  ┌─────────────────┐    ┌─────────────────┐   ┌─────────────────┐     │
│  │   🚪 API        │    │   ⚙️  Config    │   │   📡 Service    │     │
│  │   Gateway       │    │   Server        │   │   Registry      │     │
│  │   (Port 8080)   │    │   (Port 8888)   │   │   (Eureka)      │     │
│  │                 │    │                 │   │   (Port 8761)   │     │
│  │ • Routing       │    │ • External      │   │ • Discovery     │     │
│  │ • Load Balance  │    │   Config        │   │ • Health Check  │     │
│  │ • Rate Limiting │    │ • Environment   │   │ • Load Balance  │     │
│  │ • Authentication│    │   Specific      │   │ • Failover      │     │
│  └─────────────────┘    └─────────────────┘   └─────────────────┘     │
│           │                       │                      │            │
│           │                       │                      │            │
│  ━━━━━━━━━┿━━━━━━━━━━━━━━━━━━━━━━━┿━━━━━━━━━━━━━━━━━━━━━━┿━━━━━━━━━━━ │
│           │                       │                      │            │
│  📱 BUSINESS SERVICES LAYER       │                      │            │
│           │                       │                      │            │
│  ┌────────▼─────────┐    ┌─────────▼───────┐   ┌─────────▼──────────┐ │
│  │   👤 USER        │    │   🛒 ORDER      │   │   💳 PAYMENT       │ │
│  │   SERVICE        │    │   SERVICE       │   │   SERVICE          │ │
│  │   (Port 8081)    │    │   (Port 8082)   │   │   (Port 8083)      │ │
│  │                  │    │                 │   │                    │ │
│  │ ┌──────────────┐ │    │ ┌─────────────┐ │   │ ┌────────────────┐ │ │
│  │ │ Controllers  │ │    │ │Controllers  │ │   │ │ Controllers    │ │ │
│  │ │ Services     │ │    │ │Services     │ │   │ │ Services       │ │ │
│  │ │ Repositories │ │    │ │Repositories │ │   │ │ Repositories   │ │ │
│  │ └──────────────┘ │    │ └─────────────┘ │   │ └────────────────┘ │ │
│  │                  │    │                 │   │                    │ │
│  │ Features:        │    │ Features:       │   │ Features:          │ │
│  │ • User CRUD      │    │ • Order CRUD    │   │ • Payment Process  │ │
│  │ • Authentication │    │ • Inventory     │   │ • Transaction Log  │ │
│  │ • Profile Mgmt   │    │ • Order Status  │   │ • Billing          │ │
│  │ • Validation     │    │ • Notifications │   │ • Refunds          │ │
│  └──────┬───────────┘    └─────────┬───────┘   └──────────┬─────────┘ │
│         │                          │                      │           │
│  🗄️  DATA LAYER                    │                      │           │
│         │                          │                      │           │
│  ┌──────▼───────────┐    ┌─────────▼───────┐   ┌──────────▼─────────┐ │
│  │  🐘 PostgreSQL   │    │  🐘 PostgreSQL  │   │  🐘 PostgreSQL     │ │
│  │  User Database   │    │  Order Database │   │  Payment Database  │ │
│  │  (Port 5432)     │    │  (Port 5433)    │   │  (Port 5434)       │ │
│  │                  │    │                 │   │                    │ │
│  │ Tables:          │    │ Tables:         │   │ Tables:            │ │
│  │ • users          │    │ • orders        │   │ • payments         │ │
│  │ • profiles       │    │ • order_items   │   │ • transactions     │ │
│  │ • addresses      │    │ • inventory     │   │ • billing_info     │ │
│  │ • user_roles     │    │ • suppliers     │   │ • refunds          │ │
│  └──────────────────┘    └─────────────────┘   └────────────────────┘ │
│                                                                       │
└───────────────────────────────────────────────────────────────────────┘

Benefits: ✅ Independent deployment  ✅ Technology diversity  
          ✅ Fault isolation         ✅ Team autonomy
          ✅ Scalable per service    ✅ Easier testing

Communication: 
┌──────────────────────────────────────────────────────────────────────┐
│  🔄 SERVICE-TO-SERVICE COMMUNICATION                                 │
│                                                                      │
│ User Service ──HTTP/REST──► Order Service ──HTTP/REST──►  Payment    │
│      │                           │                        Service    │
│      │                           │                            │      │
│      │                           │                            │      │
│      ▼                           ▼                            ▼      │
│ Event Bus ◄────────────── Event Bus ◄─────────────── Event Bus       │
│ (Async)                     (Async)                     (Async)      │
│                                                                      │
│ Patterns Used:                                                       │
│ • 🔄 Synchronous: REST API calls for immediate responses             │
│ • 📨 Asynchronous: Event-driven for non-blocking operations          │
│ • 🛡️  Circuit Breaker: Fault tolerance and fallback mechanisms       │
│ • 🔍 Service Discovery: Automatic service location and health        │
│  monitoring                                                          │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 🔧 Dependencies for Microservices

### Complete pom.xml for Microservices

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.0</version>
        <relativePath/>
    </parent>
    
    <groupId>com.example</groupId>
    <artifactId>microservices-parent</artifactId>
    <version>1.0.0</version>
    <packaging>pom</packaging>
    
    <properties>
        <java.version>17</java.version>
        <spring-cloud.version>2023.0.0</spring-cloud.version>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>
    
    <dependencies>
        <!-- Core Spring Boot -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
        
        <!-- Database -->
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>
        
        <!-- Spring Cloud Core -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter</artifactId>
        </dependency>
        
        <!-- Service Discovery (Eureka) -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        
        <!-- For Eureka Server (only in eureka-server module) -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
        
        <!-- API Gateway -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
        
        <!-- Configuration Management -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        
        <!-- Circuit Breaker & Resilience -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-circuitbreaker-resilience4j</artifactId>
        </dependency>
        
        <!-- Load Balancing -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-loadbalancer</artifactId>
        </dependency>
        
        <!-- Service Communication -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-webflux</artifactId>
        </dependency>
        
        <!-- Distributed Tracing -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-sleuth</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-sleuth-zipkin</artifactId>
        </dependency>
        
        <!-- Metrics & Monitoring -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        
        <dependency>
            <groupId>io.micrometer</groupId>
            <artifactId>micrometer-registry-prometheus</artifactId>
        </dependency>
        
        <!-- Security -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-oauth2-resource-server</artifactId>
        </dependency>
        
        <!-- Testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-contract-stub-runner</artifactId>
            <scope>test</scope>
        </dependency>
        
        <!-- Documentation -->
        <dependency>
            <groupId>org.springdoc</groupId>
            <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
            <version>2.2.0</version>
        </dependency>
        
        <!-- Development Tools -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
    </dependencies>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

---

## 🎯 Step-by-Step Microservices Conversion

### Phase 1: Create Service Discovery Server (Eureka)

#### 1.1 Create Eureka Server Module

**File**: `eureka-server/src/main/java/com/example/eurekaserver/EurekaServerApplication.java`
```java
package com.example.eurekaserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

**File**: `eureka-server/src/main/resources/application.yml`
```yaml
server:
  port: 8761

spring:
  application:
    name: eureka-server

eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false    # Don't register itself
    fetch-registry: false          # Don't fetch registry
    service-url:
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
  server:
    wait-time-in-ms-when-sync-empty: 0    # Don't wait for replicas
    enable-self-preservation: false       # Disable in development
```

### Phase 2: Create Configuration Server

#### 2.1 Config Server Implementation

**File**: `config-server/src/main/java/com/example/configserver/ConfigServerApplication.java`
```java
package com.example.configserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.config.server.EnableConfigServer;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableConfigServer
@EnableEurekaClient
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

**File**: `config-server/src/main/resources/application.yml`
```yaml
server:
  port: 8888

spring:
  application:
    name: config-server
  
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-username/microservices-config
          default-label: main
          clone-on-start: true
        # Alternative: Use local file system
        # native:
        #   search-locations: classpath:/config

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

### Phase 3: Convert User Service to Microservice

#### 3.1 User Service Application

**File**: `user-service/src/main/java/com/example/userservice/UserServiceApplication.java`
```java
package com.example.userservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;
import org.springframework.cloud.openfeign.EnableFeignClients;

@SpringBootApplication
@EnableEurekaClient
@EnableFeignClients
public class UserServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }
}
```

#### 3.2 User Service Configuration

**File**: `user-service/src/main/resources/application.yml`
```yaml
server:
  port: 8081

spring:
  application:
    name: user-service
  
  config:
    import: "configserver:http://localhost:8888"
  
  datasource:
    url: jdbc:postgresql://localhost:5432/user_service_db
    username: springboot_user
    password: springboot_password
    driver-class-name: org.postgresql.Driver
  
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        format_sql: true

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
  instance:
    prefer-ip-address: true
    instance-id: ${spring.application.name}:${vcap.application.instance_id:${spring.application.instance_id:${random.value}}}

# Circuit Breaker Configuration
resilience4j:
  circuitbreaker:
    instances:
      external-service:
        registerHealthIndicator: true
        slidingWindowSize: 10
        minimumNumberOfCalls: 5
        permittedNumberOfCallsInHalfOpenState: 3
        automaticTransitionFromOpenToHalfOpenEnabled: true
        waitDurationInOpenState: 5s
        failureRateThreshold: 50
        eventConsumerBufferSize: 10

# Actuator Configuration
management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: always
```

#### 3.3 Enhanced User Controller with Circuit Breaker

**File**: `user-service/src/main/java/com/example/userservice/controller/UserController.java`
```java
package com.example.userservice.controller;

import com.example.userservice.model.User;
import com.example.userservice.service.UserService;
import io.github.resilience4j.circuitbreaker.annotation.CircuitBreaker;
import io.github.resilience4j.timelimiter.annotation.TimeLimiter;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import javax.validation.Valid;
import java.util.List;
import java.util.concurrent.CompletableFuture;

@RestController
@RequestMapping("/api/users")
@CrossOrigin(origins = "*")
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping
    @CircuitBreaker(name = "user-service", fallbackMethod = "getAllUsersFallback")
    public ResponseEntity<List<User>> getAllUsers() {
        List<User> users = userService.getAllUsers();
        return ResponseEntity.ok(users);
    }

    @GetMapping("/{id}")
    @CircuitBreaker(name = "user-service", fallbackMethod = "getUserByIdFallback")
    public ResponseEntity<User> getUserById(@PathVariable Long id) {
        User user = userService.getUserById(id);
        return ResponseEntity.ok(user);
    }

    @PostMapping
    @CircuitBreaker(name = "user-service", fallbackMethod = "createUserFallback")
    public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
        User savedUser = userService.saveUser(user);
        return ResponseEntity.status(HttpStatus.CREATED).body(savedUser);
    }

    @PutMapping("/{id}")
    @CircuitBreaker(name = "user-service", fallbackMethod = "updateUserFallback")
    public ResponseEntity<User> updateUser(@PathVariable Long id, @Valid @RequestBody User user) {
        User updatedUser = userService.updateUser(id, user);
        return ResponseEntity.ok(updatedUser);
    }

    @DeleteMapping("/{id}")
    @CircuitBreaker(name = "user-service", fallbackMethod = "deleteUserFallback")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
        return ResponseEntity.noContent().build();
    }

    // Fallback Methods
    public ResponseEntity<List<User>> getAllUsersFallback(Exception ex) {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE)
                .body(List.of());
    }

    public ResponseEntity<User> getUserByIdFallback(Long id, Exception ex) {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE).build();
    }

    public ResponseEntity<User> createUserFallback(User user, Exception ex) {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE).build();
    }

    public ResponseEntity<User> updateUserFallback(Long id, User user, Exception ex) {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE).build();
    }

    public ResponseEntity<Void> deleteUserFallback(Long id, Exception ex) {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE).build();
    }
}
```

### Phase 4: Create API Gateway

#### 4.1 API Gateway Application

**File**: `api-gateway/src/main/java/com/example/apigateway/ApiGatewayApplication.java`
```java
package com.example.apigateway;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableEurekaClient
public class ApiGatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(ApiGatewayApplication.class, args);
    }
}
```

#### 4.2 Gateway Configuration

**File**: `api-gateway/src/main/resources/application.yml`
```yaml
server:
  port: 8080

spring:
  application:
    name: api-gateway
  
  cloud:
    gateway:
      default-filters:
        - DedupeResponseHeader=Access-Control-Allow-Credentials Access-Control-Allow-Origin
      globalcors:
        corsConfigurations:
          '[/**]':
            allowedOrigins: "*"
            allowedMethods: "*"
            allowedHeaders: "*"
      
      routes:
        # User Service Routes
        - id: user-service
          uri: lb://user-service
          predicates:
            - Path=/api/users/**
          filters:
            - name: CircuitBreaker
              args:
                name: user-service
                fallbackUri: forward:/fallback/users
            - name: RequestRateLimiter
              args:
                redis-rate-limiter.replenishRate: 10
                redis-rate-limiter.burstCapacity: 20
                redis-rate-limiter.requestedTokens: 1
        
        # Future Order Service Routes
        - id: order-service
          uri: lb://order-service
          predicates:
            - Path=/api/orders/**
          filters:
            - name: CircuitBreaker
              args:
                name: order-service
                fallbackUri: forward:/fallback/orders

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/

# Logging
logging:
  level:
    org.springframework.cloud.gateway: DEBUG
    org.springframework.web.reactive: DEBUG
```

#### 4.3 Fallback Controller

**File**: `api-gateway/src/main/java/com/example/apigateway/controller/FallbackController.java`
```java
package com.example.apigateway.controller;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Map;

@RestController
@RequestMapping("/fallback")
public class FallbackController {

    @GetMapping("/users")
    public ResponseEntity<Map<String, String>> userServiceFallback() {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE)
                .body(Map.of(
                    "message", "User service is currently unavailable",
                    "status", "503",
                    "timestamp", String.valueOf(System.currentTimeMillis())
                ));
    }

    @GetMapping("/orders")
    public ResponseEntity<Map<String, String>> orderServiceFallback() {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE)
                .body(Map.of(
                    "message", "Order service is currently unavailable",
                    "status", "503",
                    "timestamp", String.valueOf(System.currentTimeMillis())
                ));
    }
}
```

### Phase 5: Service Communication with Feign Client

#### 5.1 Feign Client Configuration

**File**: `user-service/src/main/java/com/example/userservice/client/NotificationClient.java`
```java
package com.example.userservice.client;

import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;

@FeignClient(name = "notification-service", fallback = NotificationClientFallback.class)
public interface NotificationClient {
    
    @PostMapping("/api/notifications/send")
    void sendNotification(@RequestBody NotificationRequest request);
}

// Fallback implementation
@Component
class NotificationClientFallback implements NotificationClient {
    
    @Override
    public void sendNotification(NotificationRequest request) {
        // Log the failed notification or queue it for retry
        System.out.println("Notification service unavailable. Notification queued: " + request);
    }
}

// Request DTO
class NotificationRequest {
    private String to;
    private String subject;
    private String message;
    
    // Constructors, getters, setters
}
```

---

## 🐳 Docker Compose for Microservices

### Complete docker-compose.yml

```yaml
version: '3.8'

services:
  # PostgreSQL for User Service
  user-postgres:
    image: postgres:15.4-alpine
    container_name: user_postgres
    restart: unless-stopped
    environment:
      POSTGRES_DB: user_service_db
      POSTGRES_USER: springboot_user
      POSTGRES_PASSWORD: springboot_password
      PGDATA: /data/postgres
    volumes:
      - user_postgres_data:/data/postgres
    ports:
      - "5432:5432"
    networks:
      - microservices-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U springboot_user -d user_service_db"]
      interval: 30s
      timeout: 10s
      retries: 3

  # PostgreSQL for Order Service
  order-postgres:
    image: postgres:15.4-alpine
    container_name: order_postgres
    restart: unless-stopped
    environment:
      POSTGRES_DB: order_service_db
      POSTGRES_USER: springboot_user
      POSTGRES_PASSWORD: springboot_password
      PGDATA: /data/postgres
    volumes:
      - order_postgres_data:/data/postgres
    ports:
      - "5433:5432"
    networks:
      - microservices-network

  # Redis for Rate Limiting and Caching
  redis:
    image: redis:7-alpine
    container_name: microservices_redis
    restart: unless-stopped
    ports:
      - "6379:6379"
    networks:
      - microservices-network
    command: redis-server --appendonly yes
    volumes:
      - redis_data:/data

  # Zipkin for Distributed Tracing
  zipkin:
    image: openzipkin/zipkin
    container_name: zipkin
    restart: unless-stopped
    ports:
      - "9411:9411"
    networks:
      - microservices-network

  # Eureka Server
  eureka-server:
    build: ./eureka-server
    container_name: eureka_server
    restart: unless-stopped
    ports:
      - "8761:8761"
    networks:
      - microservices-network
    environment:
      - JAVA_OPTS=-Xmx512m -Xms256m
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8761/actuator/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  # Config Server
  config-server:
    build: ./config-server
    container_name: config_server
    restart: unless-stopped
    ports:
      - "8888:8888"
    networks:
      - microservices-network
    depends_on:
      eureka-server:
        condition: service_healthy
    environment:
      - EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://eureka-server:8761/eureka/
      - JAVA_OPTS=-Xmx512m -Xms256m

  # User Service
  user-service:
    build: ./user-service
    container_name: user_service
    restart: unless-stopped
    ports:
      - "8081:8081"
    networks:
      - microservices-network
    depends_on:
      - user-postgres
      - eureka-server
      - config-server
      - zipkin
    environment:
      - SPRING_DATASOURCE_URL=jdbc:postgresql://user-postgres:5432/user_service_db
      - SPRING_DATASOURCE_USERNAME=springboot_user
      - SPRING_DATASOURCE_PASSWORD=springboot_password
      - EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://eureka-server:8761/eureka/
      - SPRING_ZIPKIN_BASE_URL=http://zipkin:9411
      - JAVA_OPTS=-Xmx768m -Xms512m
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8081/actuator/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  # API Gateway
  api-gateway:
    build: ./api-gateway
    container_name: api_gateway
    restart: unless-stopped
    ports:
      - "8080:8080"
    networks:
      - microservices-network
    depends_on:
      - eureka-server
      - user-service
      - redis
    environment:
      - EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://eureka-server:8761/eureka/
      - SPRING_REDIS_HOST=redis
      - SPRING_REDIS_PORT=6379
      - SPRING_ZIPKIN_BASE_URL=http://zipkin:9411
      - JAVA_OPTS=-Xmx512m -Xms256m

  # pgAdmin for Database Management
  pgadmin:
    image: dpage/pgadmin4:7.8
    container_name: microservices_pgadmin
    restart: unless-stopped
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin
    ports:
      - "5050:80"
    networks:
      - microservices-network
    depends_on:
      - user-postgres
      - order-postgres

# Named volumes for data persistence
volumes:
  user_postgres_data:
    driver: local
  order_postgres_data:
    driver: local
  redis_data:
    driver: local

# Custom network for service communication
networks:
  microservices-network:
    driver: bridge
```

### Docker Build Scripts

**File**: `build-all.sh`
```bash
#!/bin/bash

echo "🏗️  Building all microservices..."

# Build Eureka Server
echo "📡 Building Eureka Server..."
cd eureka-server
./mvnw clean package -DskipTests
cd ..

# Build Config Server
echo "⚙️  Building Config Server..."
cd config-server
./mvnw clean package -DskipTests
cd ..

# Build User Service
echo "👤 Building User Service..."
cd user-service
./mvnw clean package -DskipTests
cd ..

# Build API Gateway
echo "🚪 Building API Gateway..."
cd api-gateway
./mvnw clean package -DskipTests
cd ..

echo "✅ All services built successfully!"
echo "🚀 Run 'docker-compose up -d' to start all services"
```

---

## 📚 Essential Microservices References

### 📖 Official Spring Cloud Documentation

| Component | Documentation | Purpose |
|-----------|--------------|---------|
| **Spring Cloud Gateway** | https://docs.spring.io/spring-cloud-gateway/docs/current/reference/html/ | API Gateway and routing |
| **Spring Cloud Netflix** | https://docs.spring.io/spring-cloud-netflix/docs/current/reference/html/ | Service discovery (Eureka) |
| **Spring Cloud Config** | https://docs.spring.io/spring-cloud-config/docs/current/reference/html/ | External configuration |
| **Spring Cloud Circuit Breaker** | https://docs.spring.io/spring-cloud-circuitbreaker/docs/current/reference/html/ | Fault tolerance |
| **Spring Cloud OpenFeign** | https://docs.spring.io/spring-cloud-openfeign/docs/current/reference/html/ | Service communication |
| **Spring Cloud Sleuth** | https://docs.spring.io/spring-cloud-sleuth/docs/current/reference/html/ | Distributed tracing |

### 🎯 Key Microservices Patterns

#### 1. Service Discovery Pattern
```java
// Eureka Server
@EnableEurekaServer
@SpringBootApplication
public class EurekaServerApplication { }

// Eureka Client
@EnableEurekaClient
@SpringBootApplication
public class UserServiceApplication { }
```

#### 2. API Gateway Pattern
```java
// Gateway Routes Configuration
@Configuration
public class GatewayConfig {
    
    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder builder) {
        return builder.routes()
            .route("user-service", r -> r.path("/api/users/**")
                .uri("lb://user-service"))
            .route("order-service", r -> r.path("/api/orders/**")
                .uri("lb://order-service"))
            .build();
    }
}
```

#### 3. Circuit Breaker Pattern
```java
@Service
public class UserService {
    
    @CircuitBreaker(name = "external-service", fallbackMethod = "fallbackMethod")
    @TimeLimiter(name = "external-service")
    public CompletableFuture<String> callExternalService() {
        return CompletableFuture.supplyAsync(() -> {
            // External service call
            return restTemplate.getForObject("http://external-service/api/data", String.class);
        });
    }
    
    public CompletableFuture<String> fallbackMethod(Exception ex) {
        return CompletableFuture.supplyAsync(() -> "Fallback response");
    }
}
```

#### 4. Configuration Management Pattern
```java
// Config Server
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication { }

// Config Client
@RefreshScope
@RestController
public class ConfigController {
    
    @Value("${app.message:Default Message}")
    private String message;
    
    @GetMapping("/config")
    public String getConfig() {
        return message;
    }
}
```

#### 5. Service Communication Pattern
```java
// Feign Client
@FeignClient(name = "user-service")
public interface UserClient {
    
    @GetMapping("/api/users/{id}")
    User getUserById(@PathVariable Long id);
    
    @PostMapping("/api/users")
    User createUser(@RequestBody User user);
}

// Usage in Service
@Service
public class OrderService {
    
    @Autowired
    private UserClient userClient;
    
    public Order createOrder(CreateOrderRequest request) {
        User user = userClient.getUserById(request.getUserId());
        // Process order...
    }
}
```

### 🛠️ Advanced Microservices Tools

#### Monitoring and Observability
- **Spring Boot Actuator**: Health checks, metrics
- **Micrometer + Prometheus**: Metrics collection
- **Zipkin/Jaeger**: Distributed tracing
- **ELK Stack**: Centralized logging

#### Security
- **Spring Security OAuth2**: Authentication/Authorization
- **JWT**: Token-based security
- **Vault**: Secret management

#### Data Management
- **Database per Service**: Each service owns its data
- **Event Sourcing**: Store events instead of current state
- **CQRS**: Command Query Responsibility Segregation
- **Saga Pattern**: Distributed transactions

### 📚 Learning Resources & Books

#### Essential Reading
1. **"Microservices Patterns"** by Chris Richardson
2. **"Building Microservices"** by Sam Newman
3. **"Spring Microservices in Action"** by John Carnell
4. **"Cloud Native Java"** by Josh Long & Kenny Bastani

#### Online Resources
- **Spring Cloud Documentation**: https://spring.io/projects/spring-cloud
- **Microservices.io**: https://microservices.io/patterns/
- **Spring Boot Guides**: https://spring.io/guides
- **Baeldung Spring Cloud**: https://www.baeldung.com/spring-cloud

#### Video Tutorials
- **Spring Developer YouTube**: https://www.youtube.com/c/SpringSourceDev
- **Josh Long's Spring Tips**: https://spring.io/blog/category/spring-tips

---

## 🎯 Best Practices and Patterns

### 🏗️ Design Principles

#### 1. Single Responsibility Principle
- Each microservice should have one business responsibility
- Services should be cohesive and loosely coupled
- Domain-driven design approach

#### 2. Database per Service
```sql
-- User Service Database
CREATE DATABASE user_service_db;

-- Order Service Database  
CREATE DATABASE order_service_db;

-- Payment Service Database
CREATE DATABASE payment_service_db;
```

#### 3. API First Design
```yaml
# OpenAPI Specification Example
openapi: 3.0.0
info:
  title: User Service API
  version: 1.0.0
paths:
  /api/users:
    get:
      summary: Get all users
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
```

### 🔒 Security Best Practices

#### 1. OAuth2 + JWT Implementation
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(authz -> authz
                .requestMatchers("/api/public/**").permitAll()
                .requestMatchers("/api/users/**").hasRole("USER")
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .oauth2ResourceServer(oauth2 -> oauth2
                .jwt(jwt -> jwt.decoder(jwtDecoder()))
            );
        return http.build();
    }
}
```

#### 2. Service-to-Service Authentication
```java
@Configuration
public class ServiceSecurityConfig {
    
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate() {
        RestTemplate restTemplate = new RestTemplate();
        restTemplate.getInterceptors().add(new ServiceTokenInterceptor());
        return restTemplate;
    }
}
```

### 📊 Monitoring and Observability

#### 1. Health Checks
```java
@Component
public class CustomHealthIndicator implements HealthIndicator {
    
    @Override
    public Health health() {
        // Check external dependencies
        boolean isHealthy = checkDatabaseConnection() && checkExternalService();
        
        if (isHealthy) {
            return Health.up()
                .withDetail("database", "Available")
                .withDetail("external-service", "Available")
                .build();
        } else {
            return Health.down()
                .withDetail("database", "Unavailable")
                .build();
        }
    }
}
```

#### 2. Custom Metrics
```java
@Service
public class UserService {
    
    private final Counter userCreationCounter;
    private final Timer userRetrievalTimer;
    
    public UserService(MeterRegistry meterRegistry) {
        this.userCreationCounter = Counter.builder("users.created")
            .description("Number of users created")
            .register(meterRegistry);
            
        this.userRetrievalTimer = Timer.builder("users.retrieval.time")
            .description("Time taken to retrieve users")
            .register(meterRegistry);
    }
    
    public User createUser(User user) {
        userCreationCounter.increment();
        return userRepository.save(user);
    }
    
    public List<User> getAllUsers() {
        return userRetrievalTimer.recordCallable(() -> userRepository.findAll());
    }
}
```

### 🚀 Deployment Strategies

#### 1. Blue-Green Deployment
```yaml
# Blue Environment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: user-service
      version: blue
  template:
    metadata:
      labels:
        app: user-service
        version: blue
    spec:
      containers:
      - name: user-service
        image: user-service:v1.0.0
```

#### 2. Canary Deployment
```yaml
# Canary Deployment with Istio
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: user-service
spec:
  http:
  - match:
    - headers:
        canary:
          exact: "true"
    route:
    - destination:
        host: user-service
        subset: canary
  - route:
    - destination:
        host: user-service
        subset: stable
      weight: 90
    - destination:
        host: user-service
        subset: canary
      weight: 10
```

### 🎯 Migration Checklist

#### Phase 1: Preparation
- [ ] Identify service boundaries
- [ ] Design API contracts
- [ ] Set up CI/CD pipelines
- [ ] Create monitoring strategy

#### Phase 2: Infrastructure
- [ ] Set up service discovery (Eureka)
- [ ] Configure API Gateway
- [ ] Implement configuration management
- [ ] Set up distributed tracing

#### Phase 3: Service Migration
- [ ] Extract first microservice
- [ ] Implement service communication
- [ ] Add circuit breakers
- [ ] Implement security

#### Phase 4: Operations
- [ ] Set up monitoring and alerting
- [ ] Implement logging strategy
- [ ] Create runbooks
- [ ] Train team on operations

---

## 🎉 Conclusion

This guide provides a comprehensive roadmap for learning Spring Boot annotations and converting your monolithic application to microservices architecture. Remember:

### Key Takeaways:
- **Start Small**: Convert one service at a time
- **Monitor Everything**: Implement observability from day one
- **Secure by Design**: Build security into each service
- **Test Thoroughly**: Use contract testing between services
- **Document Well**: Maintain clear API documentation

### Next Steps:
1. Master the annotations in your current application
2. Set up the infrastructure components (Eureka, Gateway)
3. Extract your first microservice
4. Gradually migrate remaining functionality
5. Implement monitoring and security

Happy coding with Spring Boot and Microservices! 🚀

---

*Last Updated: December 2024*
*Spring Boot Version: 3.2.0*
*Spring Cloud Version: 2023.0.0*
