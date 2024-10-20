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
