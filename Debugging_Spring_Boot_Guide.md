# Debugging a Spring Boot Application

This guide explains how to start a **Spring Boot** application in **debug mode** using different methods.

## 1. Start in Debug Mode with Maven
Run the following command in your project directory:
```sh
mvn spring-boot:run -Dspring-boot.run.jvmArguments="-Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=5005,suspend=n"
```

### Explanation:
- `server=y` → Starts the debug server.
- `transport=dt_socket` → Uses socket transport.
- `address=5005` → Listens on port 5005.
- `suspend=n` → Starts without waiting for the debugger.

## 2. Start in Debug Mode with Gradle
If you are using **Gradle**, run:
```sh
./gradlew bootRun --debug-jvm
```

## 3. Start in Debug Mode Using `java -jar`
If your application is packaged as a JAR, start it with:
```sh
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=5005,suspend=n -jar -jar target/trading-framework-ai-1.0.0-SNAPSHOT.jar
```

## 4. Enable Debugging in `application.properties`
Add the following to `src/main/resources/application.properties`:
```properties
debug=true
```

## 5. Using Environment Variables
You can also set the debug flags using an environment variable:
```sh
export JAVA_TOOL_OPTIONS="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"
```

## 6. Debugging in IntelliJ IDEA
1. Go to **Run > Edit Configurations**.
2. Add a **Remote JVM Debug Configuration**.
3. Set **port** to `5005`.
4. Start your Spring Boot app in debug mode (`mvn spring-boot:run` or `java -jar`).

5. Click **Debug** in IntelliJ.

## 7. Debugging in VS Code
1. Open `launch.json` in `.vscode` and add:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "request": "attach",
      "name": "Attach to Spring Boot",
      "hostName": "localhost",
      "port": 5005
    }
  ]
}
```
2. Run the app with:
```sh
mvn spring-boot:run -Dspring-boot.run.jvmArguments="-Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=5005,suspend=n"
```
3. Start debugging in VS Code.

---
### Need More Help?
If you have issues, check your **firewall settings**, ensure the **port 5005** is open, and verify that your **IDE is set to remote debugging mode**. 🚀
