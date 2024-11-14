## Guide for Installing Jenkins on an Ubuntu system

Reference Link - [Installing Jenkins on an Ubuntu](https://www.jenkins.io/doc/book/installing/linux/)

# Jenkins Installation Guide on Ubuntu

## Step 1: Install Java

1. **Update Package List:**
   ```bash
   sudo apt update
   ```

2. **Install Java Development Kit (JDK):**
   
   - This will Insatll The `Java Development Kit` for developers to run Java Programs(java code)
   ```bash
   sudo apt-get install openjdk-17-jdk-headless -y
   ```

   ```bash
   sudo apt-get install fontconfig openjdk-17-jdk
   ```

   - These will Install the `Java Runtime Environments` for running Java bassed Applications 

   ```bash
   sudo apt-get install openjdk-17-jre-headless
   ```

   ```bash
   sudo apt install fontconfig openjdk-17-jre
   ```

   - For applicatinons Using GUI use `-fontconfig` command
   - For applicatinons Not using GUI use `-headless` command 

3. **Verify Java Installation:**
   ```bash
   java -version
   ```

   ```bash
   javac -version
   ```

## Step 2: Add Jenkins Repository Key

1. **Download and Add Jenkins Repository Key:**
   ```bash
   sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
     https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
   ```

## Step 3: Add Jenkins Repository

1. **Add Jenkins Repository to Sources List:**
   ```bash
   echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
     https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
     /etc/apt/sources.list.d/jenkins.list > /dev/null
   ```

## Step 4: Install Jenkins

1. **Update Package List:**
   ```bash
   sudo apt-get update
   ```

2. **Install Jenkins:**
   ```bash
   sudo apt-get install jenkins -y
   ```

## Step 5: Verify Jenkins Installation

1. **Check Jenkins Service Status:**
   ```bash
   sudo systemctl status jenkins
   ```

## Step 6: Access Jenkins

1. **Open Jenkins in a Browser:**
   - Visit: `http://localhost:8080` or `http://<your-ip-address>:8080`

## Additional Steps

1. **Configure Security Group/Firewall:**
   - Ensure the inbound rule allows traffic on TCP port 8080.

2. **Retrieve Initial Admin Password:**
   ```bash
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```

   ---

## Guide for installing Jenkins on Windows
  
- Refference Link -  [Installing Jenkins](https://www.jenkins.io/doc/book/installing/)
```
   jenkins.io/downloads/
```

- Select windows
  - A Installer or .msi file will get downloaded 
  - Click the installer and follow the instructions
  - sele `Run service as LocalSystem(not recommended)
  - Test the port 8080 (If any thing running on 8080 stop it for and then run test )
