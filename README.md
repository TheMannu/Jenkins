Installing Jenkins on an Ubuntu system:

### Step 1: Install Java

1. **Update Package List:**
   ```bash
   sudo apt update
   ```

2. **Install Java Development Kit (JDK):**
   ```bash
   sudo apt-get install openjdk-17-jdk-headless
   ```
   ```bash
   sudo apt-get install fontconfig openjdk-17-jre
   ```

3. **Verify Java Installation:**
   ```bash
   java -version
   ```
output 
```
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)

```
*1. **`sudo apt install openjdk-17-jre-headless`**:*
   - This installs only the **`openjdk-17-jre-headless`** package, which is a minimal version of the Java Runtime Environment. The "headless" version omits all components needed for GUI applications (such as fonts and graphical libraries).
   
   **Purpose**: It's ideal for running Java applications on servers or systems without a GUI, saving resources and reducing the package size by not including unnecessary graphical libraries.

*1.**`sudo apt install fontconfig openjdk-17-jre`**:*
   - This command installs **two packages**:
     - **`fontconfig`**: A package that configures and manages fonts on Linux. It is necessary for applications that need to render fonts, especially graphical ones.
     - **`openjdk-17-jre`**: This is the full Java Runtime Environment (JRE) for OpenJDK 17, which includes everything needed to run Java applications with graphical user interfaces (GUIs), such as Swing and JavaFX. It includes the JRE, fonts, and libraries for GUI applications.

   **Purpose**: This is suitable if you're running Java applications that require a graphical user interface, as it installs the necessary libraries and fonts for such applications.

### Summary:
- **`openjdk-17-jre`**: Includes GUI support, fonts, and graphical libraries.
- **`openjdk-17-jre-headless`**: A minimal, non-GUI version suitable for server environments.

If you are working with headless environments like servers, the `openjdk-17-jre-headless` package is more appropriate. For desktop applications, you’ll need `openjdk-17-jre`.**

### Step 2: Add Jenkins Repository Key

1. **Download and Add Jenkins Repository Key:**
   ```bash
   curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   ```

### Step 3: Add Jenkins Repository

1. **Add Jenkins Repository to Sources List:**
   ```bash
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
   ```

### Step 4: Install Jenkins

1. **Update Package List:**
   ```bash
   sudo apt update
   ```

2. **Install Jenkins:**
   ```bash
   sudo apt install jenkins
   ```

### Step 5: Verify Jenkins Installation

1. **Check Jenkins Service Status:**
   ```bash
   sudo systemctl status jenkins
   ```

### Step 6: Access Jenkins

1. **Open Jenkins in a Browser:**
   - Visit: `http://localhost:8080` or `http://<your-ip-address>:8080`

### Additional Steps

1. **Configure Security Group/Firewall:**
   - Ensure the inbound rule allows traffic on TCP port 8080.

2. **Retrieve Initial Admin Password:**
   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```

A complete setup for Jenkins on Ubuntu!
