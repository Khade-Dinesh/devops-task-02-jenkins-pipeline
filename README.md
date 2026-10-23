# Task 2: Create a Simple Jenkins Pipeline for CI/CD

A beginner-friendly CI/CD project using **Jenkins, Docker, Git, GitHub, and Node.js**. This project automates the process of checking out source code, building a Docker image, running an automated test, and deploying the application in a Docker container.

## Project Overview

The objective of this project is to understand how a Jenkins Declarative Pipeline automates the main stages of a CI/CD workflow.

**GitHub Repository:**  
https://github.com/Khade-Dinesh/devops-task-02-jenkins-pipeline

## Technologies Used

- **Jenkins** — CI/CD automation
- **Git & GitHub** — Source code management
- **Docker** — Containerization and deployment
- **Node.js** — Application runtime
- **npm** — Dependency installation and testing
- **Ubuntu EC2** — Jenkins and Docker host environment

## Pipeline Workflow

The Jenkins pipeline consists of three stages:

### 1. Build
- Checks out the source code from GitHub.
- Builds a Docker image using the application's Dockerfile.
- Tags the image with the Jenkins build number.

### 2. Test
- Installs Node.js dependencies using `npm ci` inside a Node.js Docker container.
- Runs `npm test`.
- The current test script checks JavaScript syntax using `node --check server.js`.

### 3. Deploy
- Removes the previous application container if it exists.
- Starts a new container using the image created in the Build stage.
- Maps host port `3000` to container port `3000`.
- Configures the container to restart automatically unless stopped.

## Project Structure

```text
devops-task-02-jenkins-pipeline/
├── Jenkinsfile
├── README.md
├── screenshots/
└── app/
    ├── Dockerfile
    ├── server.js
    ├── package.json
    └── package-lock.json
```

## How to Run

### Prerequisites
- An Ubuntu server or EC2 instance
- Jenkins installed and running
- Docker installed and accessible to the Jenkins user
- A GitHub repository containing the project

### Setup
1. Clone the repository:

   ```bash
   git clone https://github.com/Khade-Dinesh/devops-task-02-jenkins-pipeline.git
   cd devops-task-02-jenkins-pipeline
   ```

2. Configure a Jenkins Pipeline job:
   - Select **Pipeline script from SCM**.
   - Choose **Git** as the SCM.
   - Set the repository URL to the GitHub repository above.
   - Set the branch to `*/main`.
   - Set the Script Path to `Jenkinsfile`.

3. Click **Build Now** to execute the pipeline.

## Verification

The pipeline completed successfully with all three stages passing.

The Docker container was verified using:

```bash
sudo docker ps
```

The application response was verified using:

```bash
curl http://localhost:3000
```

Expected response:

```text
Hello from my DevOps CI/CD pipeline!
```

## Screenshots

Add your project screenshots to the `screenshots/` directory and update the links below.

### Jenkins Pipeline Success
![Jenkins Pipeline Success](screenshots/01-jenkins-pipeline-success.png)

### Docker Container Running
![Docker Container Running](screenshots/02-docker-container-running.png)

### Application Response
![Application Response](screenshots/03-application-response.png)

### GitHub Repository
![GitHub Repository](screenshots/04-github-repository.png)

## Key Learnings

- Creating a Jenkins Declarative Pipeline using a `Jenkinsfile`
- Integrating Jenkins with GitHub
- Building Docker images automatically
- Running Node.js dependency installation and tests in Docker
- Deploying and verifying a containerized application
- Troubleshooting Git repository tracking and pipeline execution issues

## Conclusion

This project provided hands-on experience with a basic CI/CD workflow using Jenkins and Docker. The pipeline successfully built the application image, executed the configured test, and deployed the application in a running Docker container.

---

**Author:** Dinesh Khade  
**Project:** DevOps Internship — Task 2
