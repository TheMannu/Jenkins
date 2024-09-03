

## Jenkins Installation Script for Ubuntu

This script installs Jenkins on an Ubuntu system and sets up Docker integration.

### Script

```bash
#!/bin/bash

# Update the package list
sudo apt update

# Install OpenJDK 17
sudo apt install -y fontconfig openjdk-17-jre

# Wait for 20 seconds
echo "Wait for 20 sec"
sleep 20

# Check Java version
echo "java -version"

# Add Jenkins repository key and source list
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package list and install Jenkins
sudo apt-get update
sudo apt-get install -y jenkins

# Wait for 20 seconds
sleep 20

# Display Jenkins initial admin password
echo "sudo cat /var/lib/jenkins/secrets/initialAdminPassword"

# Install Docker
sudo apt install -y docker.io

# Wait for 10 seconds
sleep 10

# Add Jenkins and Ubuntu users to Docker group
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu

# Restart Docker service
sudo systemctl restart docker

# Wait for 10 seconds
sleep 10

# Test Docker installation
sudo su -
docker run hello-world
docker ps -a
exit

exit
```

### Post-Installation Steps

1. **Log in to Jenkins**:
   - Open your web browser and navigate to `http://<ec2-instance-public-ip>:8080`.

2. **Retrieve Jenkins Initial Admin Password**:
   - Run the following command to get the initial admin password:
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```

3. **Install Docker Pipeline Plugin**:
   - In Jenkins, go to **Manage Jenkins** > **Manage Plugins**.
   - In the **Available** tab, search for "Docker Pipeline".
   - Select the plugin and click the **Install** button.
   - Restart Jenkins after the plugin installation is complete.

4. **Restart Jenkins**:
   - After installing the plugin, restart Jenkins by navigating to:
     ```
     http://<ec2-instance-public-ip>:8080/restart
     ```
