# Complete Java Development Environment Setup Guide

This comprehensive guide will walk you through setting up a complete Java development environment, from installing the JDK to creating your first Maven project. Each step includes explanations of why it's necessary.

## Part 1: Installing Java (Azul Zulu JDK)

### Step 1: Download Java (Azul Zulu JDK)

#### Option 1: Download via Web Browser
1. Open your browser and go to the following download link:
   - [Azul Zulu JDK Download Page](https://www.azul.com/downloads/?package=jdk#zulu)
2. Select the appropriate version for your operating system:
   - **Windows**: `.msi` installer (recommended) or `.zip`
   - **Mac**: `.dmg` or `.tar.gz`
   - **Linux**: `.tar.gz` or `.deb/.rpm` packages
3. Download the installer for your platform and architecture (x64/ARM as needed).

**Why Azul Zulu JDK?** Azul Zulu is a certified, fully-compliant build of OpenJDK with long-term support options. It's free to use and provides enterprise-grade reliability without the licensing concerns of Oracle JDK.

#### Option 2: Download via curl
For Linux/macOS, you can use curl to download directly:

```sh
# Example for downloading Zulu JDK 17 for Linux x64
curl -O https://cdn.azul.com/zulu/bin/zulu17.42.19-ca-jdk17.0.7-linux_x64.tar.gz
```

For Windows, using PowerShell:
```powershell
# Example for downloading Zulu JDK 17 for Windows x64
curl -O https://cdn.azul.com/zulu/bin/zulu17.42.19-ca-jdk17.0.7-win_x64.zip
```

**Why use curl?** Using curl allows for automated downloads, which is useful for scripting installation processes, setting up CI/CD pipelines, or configuring multiple development machines consistently.

Note: Replace the URL with the specific version you need. You can find the exact download URL by visiting the Azul Zulu download page, selecting your version, and copying the download link.

### Step 2: Install Java

#### **Windows Installation**
1. Run the downloaded `.msi` installer.
2. Follow the installation wizard and choose the installation directory.
3. Select the option to **set JAVA_HOME** (if available in the installer).
4. Click **Finish** once the installation is complete.

**Why use the .msi installer?** The MSI installer automates the installation process and can automatically configure environment variables, making it more reliable than manual installation from ZIP files.

#### **Mac Installation**
1. Open the `.dmg` file and follow the installation steps.
2. Verify installation by running:
   ```sh
   java -version
   ```

**Why verify immediately?** Checking the Java version immediately confirms that the installation was successful and the Java executable is in your system PATH.

#### **Linux Installation**

##### **Debian/Ubuntu (.deb Package)**
```sh
sudo dpkg -i zulu<version>-linux_x64.deb
sudo apt-get update
```

**Why use dpkg?** The dpkg command installs the package and integrates it with the system's package manager, allowing for easier updates and management.

##### **RPM-based Distros (Fedora, RHEL, CentOS)**
```sh
sudo rpm -ivh zulu<version>-linux_x64.rpm
```

**Why use rpm?** Similar to dpkg, rpm integrates the installation with the system's package management, ensuring proper integration and future maintenance.

##### **Tar.gz (Manual Install)**
```sh
tar -xvzf zulu<version>-linux_x64.tar.gz
mv zulu-<version> /opt/zulu
```

**Why place in /opt?** The /opt directory is the standard location for optional software packages on Linux systems. This keeps your Java installation separate from system-managed packages.

### Step 3: Configure Environment Variables (Optional, but Recommended)

#### **Windows: Set JAVA_HOME**
If JAVA_HOME was not set automatically:
1. Open **Command Prompt** and run:
   ```sh
   setx JAVA_HOME "C:\Program Files\Zulu\zulu-<version>"
   setx PATH "%JAVA_HOME%\bin;%PATH%"
   ```
2. Restart your command prompt or system.

**Why set JAVA_HOME?** Many Java-based tools and frameworks look for the JAVA_HOME environment variable to locate the Java installation. Setting this correctly ensures compatibility with these tools and simplifies switching between different Java versions.

#### **Mac/Linux: Set JAVA_HOME**
Add the following to `~/.bashrc`, `~/.bash_profile`, or `~/.zshrc`:
```sh
export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-<version>/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```
Then, run:
```sh
source ~/.bashrc   # or source ~/.zshrc
```

**Why add to shell configuration files?** Adding to these files ensures the environment variables are set every time you open a new terminal, making the configuration persistent across sessions.

### Step 4: Verify Java Installation
Run the following command to check if Java is installed correctly:
```sh
java -version
```
Expected output (example for Java 17):
```sh
openjdk version "17.0.x" 202x-xx-xx
OpenJDK Runtime Environment (Zulu 17.XX+XX) (build 17.0.x+XX-LTS)
OpenJDK 64-Bit Server VM (Zulu 17.XX+XX) (build 17.0.x+XX-LTS, mixed mode)
```

**Why check the version again?** This verification confirms not only that Java is installed but also that your environment variables are correctly set, allowing Java to be found anywhere in your system.

### Step 5: Verify `JAVA_HOME`
To check if `JAVA_HOME` is set correctly, run:
```sh
echo %JAVA_HOME%   # Windows
echo $JAVA_HOME    # Mac/Linux
```

**Why verify JAVA_HOME separately?** Having JAVA_HOME correctly set is critical for many development tools like Maven, Gradle, and application servers. This step ensures these tools will work properly.

## Part 2: Setting Up Maven

### Step 1: Install Apache Maven

#### **Option 1: Using Package Managers**

#### **Windows**
1. Download the Maven binary zip archive from [Apache Maven website](https://maven.apache.org/download.cgi)
2. Extract the archive to a directory of your choice (e.g., `C:\Program Files\Apache\maven`)
3. Set environment variables:
   ```sh
   setx M2_HOME "C:\Program Files\Apache\maven"
   setx PATH "%M2_HOME%\bin;%PATH%"
   ```

**Why set M2_HOME?** Similar to JAVA_HOME, M2_HOME is used by various tools to locate your Maven installation. Setting it makes switching between Maven versions easier.

#### **Mac (using Homebrew)**
```sh
brew install maven
```

**Why use Homebrew?** Homebrew simplifies package management on macOS, handling dependency resolution and providing easy updates.

#### **Linux**
For Debian/Ubuntu:
```sh
sudo apt install maven
```

For Fedora/RHEL/CentOS:
```sh
sudo dnf install maven
```

**Why use package managers?** Package managers handle dependencies, installation paths, and updates automatically, making maintenance simpler.

#### **Option 2: Using curl**

For Linux/macOS:
```sh
# Download Maven
curl -O https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz

# Extract to /opt (or directory of your choice)
sudo tar xf apache-maven-3.9.6-bin.tar.gz -C /opt

# Create symbolic link (optional)
sudo ln -s /opt/apache-maven-3.9.6 /opt/maven

# Setup environment variables (add to your profile file)
echo 'export M2_HOME=/opt/maven' >> ~/.bashrc
echo 'export PATH=${M2_HOME}/bin:${PATH}' >> ~/.bashrc
source ~/.bashrc
```

**Why create a symbolic link?** The symbolic link provides a consistent path to reference your Maven installation regardless of version, making it easier to update Maven in the future without changing scripts or configurations.

For Windows (using PowerShell):
```powershell
# Download Maven
curl -O https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.zip

# Extract (replace C:\Program Files\Apache with your preferred location)
Expand-Archive -Path apache-maven-3.9.6-bin.zip -DestinationPath "C:\Program Files\Apache"

# Set environment variables
[Environment]::SetEnvironmentVariable("M2_HOME", "C:\Program Files\Apache\apache-maven-3.9.6", "User")
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Program Files\Apache\apache-maven-3.9.6\bin", "User")
```

**Why use PowerShell commands?** PowerShell's Environment variable commands make permanent changes to your user profile, ensuring the settings persist across restarts.

Note: Replace version numbers with the latest available versions as needed.

### Step 2: Verify Maven Installation
```sh
mvn -version
```

**Why verify the installation?** This confirms Maven is correctly installed and can locate your Java installation, which is essential for Maven to function properly.

## Part 3: Creating a Java Project with Maven

### Prerequisites
Ensure that you have the following installed on your system:
- **Java Development Kit (JDK)** (version 8 or later)
- **Apache Maven** (version 3 or later)
- **An internet connection** (to fetch dependencies from Maven Central Repository)

**Why the internet connection?** Maven downloads project dependencies from online repositories when you first build a project. Without internet access, the build will fail if dependencies aren't already in your local repository.

### Command to Generate a Java Project
To create a new Java project using Maven, run the following command:
```sh
mvn archetype:generate \
    -DgroupId=com.phdgroup \
    -DartifactId=java-project \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

**Why use archetypes?** Archetypes provide standardized project templates, ensuring consistent structure and configuration across all your projects. This reduces setup time and eliminates configuration errors.

### Explanation of Parameters:
- `-DgroupId=com.phdgroup`: The group ID of the project, typically following a reverse domain name pattern.
- `-DartifactId=java-project`: The artifact ID, which is the project name.
- `-DarchetypeArtifactId=maven-archetype-quickstart`: Specifies the archetype template for a basic Maven project.
- `-DinteractiveMode=false`: Runs the command in non-interactive mode, so you do not need to provide inputs manually.

**Why use non-interactive mode?** Non-interactive mode is ideal for automated scripts or when you already know all the required parameters, making project creation faster and more predictable.

### Project Structure
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

**Why this structure?** This standard Maven project structure separates application code from test code and follows Maven's convention over configuration principle. Following this structure allows Maven to automatically find and process your code without additional configuration.

### Building the Project
Navigate to the project directory:
```sh
cd java-project
```
Compile the project:
```sh
mvn compile
```

**Why separate compilation step?** The compile phase verifies your code syntax and structure without running tests or creating packages, allowing you to catch basic errors quickly.

### Running the Application
To execute the generated application, run:
```sh
mvn exec:java -Dexec.mainClass="com.phdgroup.App"
```

**Why specify the main class?** Java needs to know which class contains the entry point (main method) for your application. The exec plugin requires this information to run your application correctly.

### Running Tests
To run the unit tests:
```sh
mvn test
```

**Why run tests separately?** Testing verifies the correctness of your code before packaging. Running tests separately allows you to identify and fix issues before creating a distribution package.

### Packaging the Project
To create a JAR file:
```sh
mvn package
```
The output JAR will be located in the `target/` directory.

**Why create a JAR?** JAR files bundle your compiled classes and resources into a single file that can be distributed and executed. This is the standard distribution format for Java applications.

## Common Next Steps

### Updating Java Version in pom.xml
The default Maven quickstart archetype often uses an older Java version. Update your `pom.xml` to use a newer version:

```xml
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

**Why update Java version?** Modern Java versions provide new language features, performance improvements, and security updates. Specifying the version in pom.xml ensures all developers use the same version and that the compiler applies the correct language rules.

### Adding Dependencies
To add external libraries to your project, add them to the `<dependencies>` section in your `pom.xml`:

```xml
<dependencies>
    <!-- Existing dependencies -->
    
    <!-- Add new dependency -->
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.12.0</version>
    </dependency>
</dependencies>
```

**Why use Maven for dependencies?** Maven automatically downloads and manages dependencies, ensuring consistent versions across development environments and handling transitive dependencies (dependencies of dependencies).

### Creating an Executable JAR
To create a standalone executable JAR with all dependencies included, add the Maven Shade plugin to your `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.4.1</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <transformers>
                            <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass>com.phdgroup.App</mainClass>
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

**Why use the Shade plugin?** Standard JAR files don't include dependencies, which means your application won't run without those dependencies on the classpath. The Shade plugin creates a "fat JAR" that includes all dependencies, making distribution and execution simpler.

## Conclusion
Congratulations! You have successfully set up a complete Java development environment with Azul Zulu JDK and Maven. You can now build, test, and package Java applications using industry-standard tools and practices.

Understanding the reasons behind each step in this process will help you troubleshoot issues and customize your environment for specific project needs.
