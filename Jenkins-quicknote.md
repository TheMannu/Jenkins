
# Jenkins Overview

- **Purpose**: Automation server for CI/CD in software development.
- **Language**: Written in Java.
- **Key Features**: Automation, Continuous Integration (CI), Continuous Delivery (CD).

## Jenkins Architecture

### Master:
- Controls Jenkins environment
- Schedules and monitors build jobs

### Agent:
- Executes build scripts assigned by the master
- Reports back results to the master

## Jenkins Workflow

### Source Code Management:
- Supports Git, SVN, Mercurial, etc.
- Developers commit code changes to the repository

### Build Execution:
- Master assigns build job to agent
- Agent executes build script (e.g., Maven, Gradle)

### Testing:
- Automated tests run during the build process
- Test results recorded and reported back

### Post-Build Actions:
- Notifications sent (email, Slack)
- Successful builds deployed automatically

## Jenkins Use Cases:
- **CI/CD**: Automate code integration to production deployment
- **Testing**: Run unit, integration, and automated tests
- **Build Automation**: Compile code, run scripts, create builds automatically
- **DevOps**: Integrate with DevOps tools for streamlined processes

## Example Jenkins Pipeline (Jenkinsfile)

```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'scp target/your-app.jar user@server:/path/to/deploy'
            }
        }
    }
}
```

**Jenkins** is an open-source automation server that helps automate building, testing, and deploying software, facilitating continuous integration and continuous delivery.

## Resources
- [YouTube - Jenkins Complete Tutorial](https://www.youtube.com/watch?v=FX322RVNGj4&t=7679s)
- [YouTube - Jenkins for Beginners](https://www.youtube.com/watch?v=7KCS70sCoK0&t=718s)
- [YouTube - Jenkins Pipelines](https://www.youtube.com/watch?v=3a8KsB5wJDE)
- [CloudBees TV](https://www.youtube.com/c/CloudBeesTV)
- [YouTube - Jenkins Advanced Features](https://www.youtube.com/watch?v=Ei_Nk14vruE)
- [YouTube - Jenkins in DevOps](https://www.youtube.com/watch?v=pMO26j2OUME&list=PLy7NrYWoggjw_LIiDK1LXdNN82uYuuuiC)

## Links
- [Jenkins Official Documentation](https://www.jenkins.io/doc/)
- [Jenkins SIG Documentation](https://www.jenkins.io/sigs/docs/)
- [Jenkins User Handbook](https://www.jenkins.io/user-handbook.pdf)

## Getting Started
- **Installing Jenkins**
- **Getting started with pipelines**
- **Jenkins on AWS**
- **Jenkins Installation in Kubernetes with Helm**

---

## Jenkins in Kubernetes

### Create a Jenkins Setup in Kubernetes Using Helm
```bash
helm install jenkins jenkins/jenkins
kubectl get secret jenkins -o jsonpath='{.data.jenkins-admin-password}' | base64 --decode
kubectl port-forward service/jenkins 8080:8080 --namespace default
```

### Configure Jenkins Using Configuration as Code

```yaml
jenkins:
  systemMessage: "Welcome to Jenkins configured with JCasC!"
  securityRealm:
    local:
      allowsSignup: false
      users:
        - id: admin
          password: admin_password
  authorizationStrategy:
    loggedInUsersCanDoAnything:
      allowAnonymousRead: false
  unclassified:
    location:
      url: "http://jenkins.example.com/"
  tool:
    git:
      installations:
        - name: "Default Git"
          home: "/usr/bin/git"
  credentials:
    system:
      domainCredentials:
        - credentials:
            - basicSSHUserPrivateKey:
                scope: SYSTEM
                id: "git-ssh-key"
                username: "git"
                privateKeySource:
                  directEntry:
                    privateKey: |
                      -----BEGIN RSA PRIVATE KEY-----
                      [Your SSH private key]
                      -----END RSA PRIVATE KEY-----
```

### Run Jenkins Jobs as Ephemeral Pods in Kubernetes

```groovy
pipeline {
    agent {
        kubernetes {
            yaml """
            apiVersion: v1
            kind: Pod
            metadata:
              labels:
                jenkins: ephemeral
            spec:
              containers:
                - name: jnlp
                  image: jenkins/jnlp-slave
                  tty: true
            """
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Hello World!'
            }
        }
    }
}
```

### Write Your First Jenkinsfile to Run a Basic Test to Calculate Pi

```groovy
pipeline {
    agent any
    stages {
        stage('Calculate Pi') {
            steps {
                script {
                    def pi = 0
                    def n = 10000 // Number of iterations
                    for (int i = 0; i < n; i++) {
                        def sign = (i % 2 == 0) ? 1 : -1
                        pi += sign * (4.0 / (2 * i + 1))
                    }
                    echo "Calculated Pi: ${pi}"
                }
            }
        }
    }
}
```

---

## Configure a Bitbucket Pipeline to Automatically Run Jenkins Job

### Configure Bitbucket Pipeline

- Open your Bitbucket repository.
- Navigate to **Settings > Pipelines > Repository settings**.
- Create or update the `bitbucket-pipelines.yml` file in your repository.

```yaml
image: node:14.17.6  # Use an appropriate Docker image

pipelines:
  branches:
    master:
      - step:
          name: Trigger Jenkins Job
          script:
            - apt-get update && apt-get install -y curl  # Install curl
            - curl -X POST "JENKINS_JOB_URL/build?token=YOUR_AUTH_TOKEN"
```

Replace `JENKINS_JOB_URL` with the actual URL of your Jenkins job and `YOUR_AUTH_TOKEN` with the authentication token.

### Commit Changes:
- Save and push changes to the Bitbucket repository.

### Test Pipeline Trigger:
- Make a commit and verify that the Jenkins job is triggered automatically.

---

## Create an Alert When Job Passed/Failed to a Slack Channel
### Install Jenkins Slack Plugin
- Use **Jenkins Plugin Manager** to install "Slack Notification" plugin.

### Configure Slack Integration
- Go to **Jenkins > Manage Jenkins > Configure System**.
- In the "Slack" section, add your Slack team details (domain, token).

### Update Jenkins Job
- Open job configuration.
- Go to **Post-build Actions > Slack Notifications**.
- Configure Slack settings and choose notification options (build start, failure, success).

### Test Notifications
- Trigger a build in Jenkins and check the Slack channel for notifications.


