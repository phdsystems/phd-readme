# Java Project Setup using Maven Archetype

## Overview
This guide provides step-by-step instructions on how to create a Java project using Maven. This is useful for setting up a basic Java application with Maven quickly.

## Prerequisites
Ensure that you have the following installed on your system:
- **Java Development Kit (JDK)** (version 8 or later)
- **Apache Maven** (version 3 or later)
- **An internet connection** (to fetch dependencies from Maven Central Repository)

## Command to Generate a Java Project
To create a new Java project using Maven, run the following command:

```sh
mvn archetype:generate \
    -DgroupId=com.phdgroup \
    -DartifactId=java-project \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

### Explanation of Parameters:
- `-DgroupId=com.phdgroup`: The group ID of the project, typically following a reverse domain name pattern.
- `-DartifactId=java-project`: The artifact ID, which is the project name.
- `-DarchetypeArtifactId=maven-archetype-quickstart`: Specifies the archetype template for a basic Maven project.
- `-DinteractiveMode=false`: Runs the command in non-interactive mode, so you do not need to provide inputs manually.

## Project Structure
After running the command, Maven generates the following directory structure:

```
java-project/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── phdgroup/
│   │   │           └── App.java
│   ├── test/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── phdgroup/
│   │   │           └── AppTest.java
```

## Building the Project
Navigate to the project directory:

```sh
cd java-project
```

Compile the project:

```sh
mvn compile
```

## Running the Application
To execute the generated application, run:

```sh
mvn exec:java -Dexec.mainClass="com.phdgroup.App"
```

## Running Tests
To run the unit tests:

```sh
mvn test
```

## Packaging the Project
To create a JAR file:

```sh
mvn package
```
The output JAR will be located in the `target/` directory.

## Conclusion
This guide walks through creating a simple Java application using Maven. You can now modify the project, add dependencies, and start developing your Java application.
