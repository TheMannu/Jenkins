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
