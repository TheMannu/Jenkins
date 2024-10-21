Troubleshooting **day-to-day Jenkins issues**, Based on common problems like configuration issues, agent problems, and plugin management. Included common problems.

### 1. **Configuration Issues**
   - **Problem**: Incomplete or wrong configurations in jobs, pipelines, or Jenkins settings.
   - **Solution**:
     - Ensure all required fields in jobs are configured properly.
     - Validate job parameters like Git repositories, build triggers, and post-build actions.
     - Regularly review Jenkins configurations in **Manage Jenkins** to check for errors or misconfigurations.
     - Use **Configuration as Code (JCasC)** to maintain consistency across Jenkins instances.


### 2. **Jobs Always Running on Master**
   - **Problem**: Jobs are not distributed to agents/slaves and always run on the master node, leading to performance issues.
   - **Solution**:
     - **Restrict jobs to run on specific nodes** by adding the **"Restrict where this project can be run"** option in job configurations.
     - Define proper **labels** for agents/slaves and assign jobs to run on these labeled nodes.
     - Avoid running non-administrative jobs on the master node to improve system stability and scalability.

### 3. **Agent/Slave is Offline**
   - **Problem**: Jenkins agents go offline, resulting in job failures or job queuing.
   - **Solution**:
     - **Check connectivity** between the master and the agent. Ensure there are no firewall, DNS, or network issues.
     - Restart the Jenkins agent, either via the Jenkins interface or by using SSH to the agent machine.
     - Ensure the agent machine has sufficient resources (CPU, memory) to handle jobs.
     - Verify agent logs (`/var/log/jenkins/jenkins.log` or agent-specific logs) to identify the root cause of disconnections.