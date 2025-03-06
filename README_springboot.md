# Spring Boot 3.4.3 Project Setup Guide (Java 17)

## Overview
This guide provides comprehensive instructions for creating a Spring Boot 3.4.3 project using Maven. Spring Boot simplifies the development of production-ready applications by providing a convention-over-configuration approach with sensible defaults.

## Prerequisites
Ensure that you have the following installed on your system:
- **Java Development Kit (JDK)** (version 17 or later, required for Spring Boot 3.x)
- **Apache Maven** (version 3.8.0 or later)
- **An internet connection** (to fetch dependencies from Maven Central Repository)
- **IDE** (Optional: IntelliJ IDEA, Eclipse, or VS Code with Spring extensions)

## Methods to Create a Spring Boot Project

### Method 1: Using Maven for Spring Boot

After testing multiple archetypes, it appears that many Spring Boot archetypes in Maven Central are either outdated or unavailable. Instead, let's use a more reliable approach with two steps:

#### Step 1: Create a basic Maven project
```sh
mvn archetype:generate \
    -DgroupId=com.phdgroup \
    -DartifactId=springboot-project \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```

#### Step 2: Convert it to a Spring Boot project (version 3.4.3 with Java 17)
After generating the basic project, navigate to the project directory and replace the contents of the `pom.xml` file with the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.4.3</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    
    <groupId>com.phdgroup</groupId>
    <artifactId>springboot-project</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springboot-project</name>
    <description>Spring Boot Project for PHD Group</description>
    
    <properties>
        <java.version>17</java.version>
    </properties>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
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

Then create a main application class in `src/main/java/com/phdgroup/App.java`:

```java
package com.phdgroup;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}

### Method 2: Using Spring Initializr (Recommended)
Spring Initializr provides a more streamlined approach to create Spring Boot projects with the dependencies you need.

#### Option A: Via Web Interface
1. Visit [https://start.spring.io/](https://start.spring.io/)
2. Configure your project:
   - Project: Maven
   - Language: Java
   - Spring Boot version: **3.4.3**
   - Java: **17**
   - Group: com.phdgroup
   - Artifact: springboot-project
   - Dependencies: Add necessary dependencies (e.g., Spring Web, Spring Data JPA, etc.)
3. Click "Generate" to download the project as a ZIP file
4. Extract the ZIP file and open the project in your IDE

#### Option B: Via Command Line
```sh
curl https://start.spring.io/starter.tgz \
  -d dependencies=web,actuator,devtools \
  -d type=maven-project \
  -d bootVersion=3.4.3 \
  -d groupId=com.phdgroup \
  -d artifactId=springboot-project \
  -d name=SpringBootProject \
  -d packageName=com.phdgroup \
  -o springboot-project.tgz
```

Then extract the archive:
```sh
mkdir springboot-project
tar -xzvf springboot-project.tgz -C springboot-project
```

## Project Structure
After creating the project, you'll have a structure similar to:

```
springboot-project/
├── pom.xml                                       # Maven configuration file
├── mvnw                                          # Maven wrapper script (Unix)
├── mvnw.cmd                                      # Maven wrapper script (Windows)
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── phdgroup/
│   │   │           ├── SpringBootProjectApplication.java  # Main application class
│   │   │           ├── controller/                        # For REST controllers
│   │   │           ├── service/                           # For business logic
│   │   │           ├── repository/                        # For data access
│   │   │           └── model/                             # For data entities
│   │   └── resources/
│   │       ├── application.properties                     # Application configuration
│   │       ├── static/                                    # Static content (CSS, JS)
│   │       └── templates/                                 # Template files (Thymeleaf, etc.)
│   └── test/
│       └── java/
│           └── com/
│               └── phdgroup/
│                   └── SpringBootProjectApplicationTests.java  # Test class
```

## Configuring Spring Boot

### Essential POM Dependencies
If you used a basic Maven Archetype (not a Spring Boot specific one), you need to add these dependencies to your `pom.xml`:

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.4.3</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

### Main Application Class
Create the main application class if not already generated:

```java
package com.phdgroup;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootProjectApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringBootProjectApplication.class, args);
    }
}
```

### Create a Simple REST Controller
Create a basic controller to verify your setup:

```java
// Java 17 compatible code with Spring Boot 3.4.3
package com.phdgroup.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    
    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot 3.4.3!";
    }
}
```

### Configure Application Properties
Edit `src/main/resources/application.properties`:

```properties
# Server configuration
server.port=8080
server.servlet.context-path=/api

# Logging
logging.level.root=INFO
logging.level.com.phdgroup=DEBUG

# Additional configurations based on your requirements
# spring.datasource.url=jdbc:mysql://localhost:3306/db_name
# spring.datasource.username=root
# spring.datasource.password=password
```

## Running the Application
Navigate to the project directory:
```sh
cd springboot-project
```

You can run the application using:

```sh
# Using Maven directly
mvn spring-boot:run

# Using Maven wrapper (if available)
./mvnw spring-boot:run   # Unix
mvnw.cmd spring-boot:run # Windows
```

Access your application at [http://localhost:8080/api/hello](http://localhost:8080/api/hello)

## Building the Project
To build an executable JAR:

```sh
mvn clean package
```

The JAR file will be located in the `target/` directory.

To run the JAR:
```sh
java -jar target/springboot-project-0.0.1-SNAPSHOT.jar
```

## Running Tests
To run tests:

```sh
mvn test
```

## Development Best Practices

1. **Use Spring Profiles**: Configure different environments (dev, test, prod)
   ```properties
   # application-dev.properties, application-prod.properties
   spring.profiles.active=dev
   ```

2. **Implement Proper Exception Handling**:
   ```java
   @ControllerAdvice
   public class GlobalExceptionHandler {
       @ExceptionHandler(Exception.class)
       public ResponseEntity<Object> handleException(Exception ex) {
           // Error handling logic
       }
   }
   ```

3. **Use Dependency Injection**: Let Spring manage your objects
   ```java
   @Service
   public class UserService {
       private final UserRepository userRepository;
       
       @Autowired
       public UserService(UserRepository userRepository) {
           this.userRepository = userRepository;
       }
   }
   ```

4. **Enable Spring Dev Tools**: For faster development cycles
   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-devtools</artifactId>
       <optional>true</optional>
   </dependency>
   ```

5. **Implement API Documentation**: With Springdoc OpenAPI
   ```xml
   <dependency>
       <groupId>org.springdoc</groupId>
       <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
       <version>2.2.0</version>
   </dependency>
   ```

## Troubleshooting Common Maven & Spring Boot Issues

### Maven Issues

1. **Dependencies not downloading**
   - Check your internet connection
   - Verify Maven repository settings in `settings.xml`
   - Try clearing Maven cache: `mvn dependency:purge-local-repository`
   - Use `mvn -U` flag to force update: `mvn clean install -U`

2. **"Plugin not found" errors**
   - Check that your Maven installation is current (Maven 3.8.x or newer recommended)
   - Verify you have the plugin repositories specified in your POM
   - Try adding pluginRepository entries to your POM

3. **Version conflicts/dependency issues**
   - Use `mvn dependency:tree` to analyze dependency hierarchy
   - Add exclusions for conflicting dependencies:
     ```xml
     <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-web</artifactId>
         <exclusions>
             <exclusion>
                 <groupId>org.springframework.boot</groupId>
                 <artifactId>spring-boot-starter-logging</artifactId>
             </exclusion>
         </exclusions>
     </dependency>
     ```
   - Consider using Maven's dependencyManagement section:
     ```xml
     <dependencyManagement>
         <dependencies>
             <dependency>
                 <groupId>org.springframework</groupId>
                 <artifactId>spring-framework-bom</artifactId>
                 <version>6.1.3</version>
                 <type>pom</type>
                 <scope>import</scope>
             </dependency>
         </dependencies>
     </dependencyManagement>
     ```

4. **Build failure due to tests**
   - Skip tests temporarily: `mvn install -DskipTests`
   - Check test logs in the `target/surefire-reports` directory
   - Verify test resources are properly configured
   - Use a specific Surefire plugin version to avoid known issues:
     ```xml
     <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-surefire-plugin</artifactId>
         <version>3.2.2</version>
     </plugin>
     ```

### Spring Boot Issues (For Spring Boot 3.4.3)

1. **Port already in use**
   - Change the port in `application.properties`:
     ```properties
     server.port=8081
     ```
   - Kill the process using the port (Windows: `netstat -ano | findstr 8080`, Linux/Mac: `lsof -i :8080`)

2. **Application not starting**
   - Check console output for detailed error messages
   - Verify all required dependencies are included
   - Check application.properties for configuration errors
   - Use `--debug` flag when starting: `mvn spring-boot:run -Dspring-boot.run.jvmArguments="--debug"`
   - Ensure Java 17+ is being used (required for Spring Boot 3.x)

3. **Bean creation errors**
   - Verify your component scanning is properly configured
   - Check for circular dependencies
   - Ensure required properties are set for @ConfigurationProperties beans
   - Use appropriate Spring annotations (@Component, @Service, @Repository)
   - For Spring Boot 3.4.3, check compatibility with Jakarta EE 10

4. **Application context failing to start**
   - Check for conflicting bean definitions
   - Verify database connections if using Spring Data
   - Look for missing required properties
   - Inspect the full stack trace for root cause
   - Check for deprecated APIs in Spring Boot 3.4.3

5. **"whitelabel" error page appears**
   - Check your controller mappings
   - Verify view resolvers are configured correctly 
   - Inspect server logs for exceptions
   - Ensure proper content-type is being returned

6. **Autowiring failures**
   - Ensure classes are in the component-scan path
   - Check for proper annotations (@Component, @Service, etc.)
   - Verify bean qualifier names if multiple implementations exist:
     ```java
     @Service
     @Qualifier("primaryUserService")
     public class PrimaryUserServiceImpl implements UserService {
         // implementation
     }
     
     @Autowired
     @Qualifier("primaryUserService")
     private UserService userService;
     ```

### Database Connectivity Issues

1. **Database connection failures**
   - Verify database credentials in application.properties:
     ```properties
     spring.datasource.url=jdbc:mysql://localhost:3306/db_name?useSSL=false&serverTimezone=UTC
     spring.datasource.username=root
     spring.datasource.password=password
     spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
     ```
   - Check that the database server is running
   - Ensure firewall rules allow the connection
   - Try connecting with an external tool to isolate Spring vs. DB issues
   - For Spring Boot 3.4.3, ensure your JDBC driver is compatible (MySQL 8.0.33+, PostgreSQL 42.6.0+)

2. **Hibernate/JPA errors**
   - Check entity annotations (@Entity, @Table, etc.)
   - Verify dialect is correct for your database version:
     ```properties
     spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
     ```
   - Review naming strategies and column mappings
   - Check for schema mismatch between entities and DB tables
   - For Spring Boot 3.4.3, use Hibernate 6.x compatible properties

### Running in Debug Mode

#### Debugging with Maven

```sh
# For Spring Boot 3.4.3 with Maven 3.8+
mvn spring-boot:run -Dspring-boot.run.jvmArguments="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005"
```

#### Debugging with Java command (JDK 17+)
```sh
# For Spring Boot 3.4.3 jar with JDK 17+
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar target/springboot-project-0.0.1-SNAPSHOT.jar
```

#### Using Spring Boot's built-in debug flag
```sh
# Spring Boot 3.4.3
java -jar target/springboot-project-0.0.1-SNAPSHOT.jar --debug
```

#### IDE Debugging

**IntelliJ IDEA 2023.3+**:
1. Create a new "Remote JVM Debug" configuration
2. Set host to "localhost" and port to "5005"
3. Set JDK to Java 17 or higher
4. Start your application with debug parameters
5. Click the debug icon to connect

**Eclipse 2023-12+**:
1. Go to Run → Debug Configurations
2. Create a new "Remote Java Application" configuration
3. Set connection properties (host: localhost, port: 5005)
4. Set JRE to JDK 17 or higher
5. Click "Debug"

**VS Code 1.85+**:
1. Install the "Spring Boot Extension Pack" version 0.36.0+
2. Create a launch.json file with remote debugging configuration:
```json
{
  "type": "java",
  "name": "Attach to Remote Program",
  "request": "attach",
  "hostName": "localhost",
  "port": 5005,
  "projectName": "springboot-project"
}
```

#### Debugging Tips

1. **Remote Debugging Production** (JDK 17+)
   - Use suspend=y to pause application until debugger connects
   - Set appropriate timeout values for your environment
   - Consider security implications of exposed debug ports
   - For Java 21/Spring Boot 3.4.3, use the new JDK Flight Recorder for profiling:
     ```sh
     java -XX:StartFlightRecording=duration=120s,filename=recording.jfr -jar target/springboot-project-0.0.1-SNAPSHOT.jar
     ```

2. **Conditional Breakpoints**
   - Set conditions on breakpoints to trigger only in specific scenarios
   - Use hit counts to skip initial iterations in loops
   - With Spring Boot 3.4.3, leverage the reactive debugging tools if using WebFlux

3. **Watching Variables**
   - Add watches for key values
   - Use evaluator to run expressions during debugging
   - For Spring Boot 3.4.3, check support for the new Java 21 features in your debugger

4. **HTTP Request Debugging**
   - Use tools like Postman v10+ or Insomnia 2023.5+ to craft specific requests
   - Enable request/response logging:
     ```properties
     # For Spring Boot 3.4.3
     logging.level.org.springframework.web=DEBUG
     logging.level.org.springframework.http.converter.json=DEBUG
     ```

5. **Thread Dumps** (JDK 17+)
   - Generate thread dumps when application hangs:
     ```sh
     jstack -l [PID] > thread-dump.txt
     ```
   - Use VisualVM 2.1+ or JConsole to monitor threads

## Conclusion
This guide walks through setting up a Spring Boot application using Maven. With this foundation, you can expand your project by adding more controllers, services, and integrating with databases or other external systems.

## Additional Resources
- [Official Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [Spring Guides](https://spring.io/guides)
