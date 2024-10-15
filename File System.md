The default paths where Jenkins stores its configuration, job data, and other operational files based on the platform it's running on.

The typical Jenkins home directory locations:

### 1. **Windows**:
   - **WAR File Install (User-based installation)**:
     - When Jenkins is run as a standalone Java application (using the `.war` file), it typically uses the user's home directory:
       ```
       C:\Users\<YourUsername>\.jenkins
       ```
     - Example: `C:\Users\Admin\.jenkins`

   - **Windows Service Install**:
     - If Jenkins is installed as a service, the home directory defaults to:
       ```
       C:\ProgramData\Jenkins\.jenkins
       ```
     - **Note**: `C:\ProgramData` is a hidden directory, so you may need to enable viewing hidden files to see it.

   - **Slave Node Configuration**:
     - If you're using a **Jenkins agent (slave)**, the agent workspace can be set to any location, but a common path is:
       ```
       C:\Dev\jenkins-slave
       ```
     - This can be configured during the setup of the Jenkins agent.

### 2. **Linux**:
   - On Linux, the default Jenkins home directory is:
     ```
     /var/jenkins_home
     ```
   - This is used when Jenkins is installed using a package manager or Docker.

### 3. **Changing the Jenkins Home Directory**:
   - You can change the Jenkins home directory by setting the `JENKINS_HOME` environment variable.
   - For example, in Windows, you can set this by:
     - Right-clicking **This PC** → **Properties** → **Advanced system settings** → **Environment Variables**.
     - Add a new **System variable** with the name `JENKINS_HOME` and the desired path (e.g., `D:\Jenkins\Home`).
   
   - For Linux, you can modify the `/etc/default/jenkins` file and set:
     ```
     JENKINS_HOME=/your/custom/path
     ```
