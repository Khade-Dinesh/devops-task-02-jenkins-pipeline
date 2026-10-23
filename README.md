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

## How to
