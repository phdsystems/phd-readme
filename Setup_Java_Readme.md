# Java Setup Guide

This guide will walk you through downloading, installing, and configuring Java using Azul Zulu JDK.

## Step 1: Download Java (Azul Zulu JDK)

1. Open your browser and go to the following download link:
   - [Azul Zulu JDK Download Page](https://www.azul.com/downloads/?package=jdk#zulu)
2. Select the appropriate version for your operating system:
   - **Windows**: `.msi` installer (recommended) or `.zip`
   - **Mac**: `.dmg` or `.tar.gz`
   - **Linux**: `.tar.gz` or `.deb/.rpm` packages
3. Download the installer for your platform and architecture (x64/ARM as needed).

## Step 2: Install Java

### **Windows Installation**
1. Run the downloaded `.msi` installer.
2. Follow the installation wizard and choose the installation directory.
3. Select the option to **set JAVA_HOME** (if available in the installer).
4. Click **Finish** once the installation is complete.

### **Mac Installation**
1. Open the `.dmg` file and follow the installation steps.
2. Verify installation by running:
   ```sh
   java -version
   ```

### **Linux Installation**
#### **Debian/Ubuntu (.deb Package)**
```sh
sudo dpkg -i zulu<version>-linux_x64.deb
sudo apt-get update
```

#### **RPM-based Distros (Fedora, RHEL, CentOS)**
```sh
sudo rpm -ivh zulu<version>-linux_x64.rpm
```

#### **Tar.gz (Manual Install)**
```sh
tar -xvzf zulu<version>-linux_x64.tar.gz
mv zulu-<version> /opt/zulu
```

## Step 3: Configure Environment Variables (Optional, but Recommended)

### **Windows: Set JAVA_HOME**
If JAVA_HOME was not set automatically:
1. Open **Command Prompt** and run:
   ```sh
   setx JAVA_HOME "C:\Program Files\Zulu\zulu-<version>"
   setx PATH "%JAVA_HOME%\bin;%PATH%"
   ```
2. Restart your command prompt or system.

### **Mac/Linux: Set JAVA_HOME**
Add the following to `~/.bashrc`, `~/.bash_profile`, or `~/.zshrc`:
```sh
export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-<version>/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH
```
Then, run:
```sh
source ~/.bashrc   # or source ~/.zshrc
```

## Step 4: Verify Java Installation
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

## Step 5: Verify `JAVA_HOME`
To check if `JAVA_HOME` is set correctly, run:
```sh
echo %JAVA_HOME%   # Windows
echo $JAVA_HOME    # Mac/Linux
```

## Conclusion
Congratulations! You have successfully installed and configured Java using Azul Zulu JDK. 🎉

You can now proceed with your Java development environment setup.
