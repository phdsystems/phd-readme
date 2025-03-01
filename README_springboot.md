# Spring Boot Project Setup using Maven Archetype

## Overview
This guide provides step-by-step instructions on how to create a Spring Boot project using Maven. This is useful for setting up a simple Spring Boot application with Maven quickly.

## Prerequisites
Ensure that you have the following installed on your system:
- **Java Development Kit (JDK)** (version 11 or later)
- **Apache Maven** (version 3 or later)
- **An internet connection** (to fetch dependencies from Maven Central Repository)

## Command to Generate a Spring Boot Project
To create a new Spring Boot project using Maven, run the following command:

```sh
mvn archetype:generate \
    -DgroupId=com.phdgroup \
    -DartifactId=springboot-project \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Alternatively, you can use Spring Initializr to generate the project:

```sh
curl https://start.spring.io/starter.tgz \
  -d dependencies=web \
  -d type=maven-project \
  -d groupId=com.phdgroup \
  -d artifactId=springboot-project \
  -d name=SpringBootProject \
  -d packageName=com.phdgroup \
  -o springboot-project.tgz
```

### Explanation of Parameters:
- `-DgroupId=com.phdgroup`: The group ID of the project, typically following a reverse domain name pattern.
- `-DartifactId=springboot-project`: The artifact ID, which is the project name.
- `-DarchetypeArtifactId=maven-archetype-quickstart`: Specifies the archetype template for a basic Maven project.
- `-DinteractiveMode=false`: Runs the command in non-interactive mode.

## Project Structure
After running the command, Maven generates the following directory structure:

```
springboot-project/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── phdgroup/
│   │   │           ├── SpringBootProjectApplication.java
│   ├── test/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── phdgroup/
│   │   │           ├── SpringBootProjectApplicationTests.java
```

## Running the Application
Navigate to the project directory:

```sh
cd springboot-project
```

Run the application:

```sh
mvn spring-boot:run
```

## Building the Project
To build the project:

```sh
mvn package
```
The output JAR file will be located in the `target/` directory.

## Running Tests
To run the unit tests:

```sh
mvn test
```

## Conclusion
This guide walks through creating a simple Spring Boot application using Maven. You can now modify the project, add dependencies, and start developing your Spring Boot application.
