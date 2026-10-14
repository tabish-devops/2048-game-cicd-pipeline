# 2048 Game CI/CD Pipeline on AWS EC2

## Project Overview

This project demonstrates a basic Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins, GitHub, Docker, and AWS EC2.

The pipeline retrieves the 2048 game application source code from GitHub, builds a Docker image, verifies the image, deploys the application as a Docker container, and checks whether the application responds successfully.

## Architecture

Developer / GitHub Repository → Jenkins Pipeline → Docker Image → Docker Container → AWS EC2

## Technologies Used

- AWS EC2 (Ubuntu)
- Git and GitHub
- Jenkins
- Jenkins Pipeline (Groovy)
- Docker
- Linux
- Nginx

## CI/CD Workflow

1. Jenkins retrieves the pipeline definition from the GitHub repository.
2. The pipeline clones the 2048 game application source code.
3. Docker builds an image using the application's Dockerfile.
4. Jenkins verifies that the image exists.
5. The pipeline replaces the previous application container and starts the new container.
6. Jenkins checks the application using an HTTP health check.

## Project Structure

```text
2048-game-cicd-pipeline/
├── Jenkinsfile
└── README.md
```

During a Jenkins build, the application source code is checked out into the `app/` directory in the Jenkins workspace.

## Deployment Details

- Cloud platform: AWS EC2
- Operating system: Ubuntu
- Container runtime: Docker
- Web server: Nginx
- Application port: 8081
- Container port: 80

Open the deployed game using:

`http://YOUR_EC2_PUBLIC_IP:8081`

Replace `YOUR_EC2_PUBLIC_IP` with the public IPv4 address of your EC2 instance.

The EC2 security group's inbound rules must allow TCP port 8081 from your intended client IP address.

## Run the Application Locally

Build the Docker image:

```bash
docker build -t shopsphere-2048:latest app
```

Run the container:

```bash
docker run -d --name shopsphere-2048 -p 8081:80 shopsphere-2048:latest
```

Open `http://localhost:8081` in your browser.

## Jenkins Pipeline

The `Jenkinsfile` defines the stages used to build, test, deploy, and verify the application.

The pipeline can be executed through the Jenkins job configured to retrieve the `Jenkinsfile` from GitHub.

## Learning Outcomes

- Understanding CI/CD concepts.
- Integrating GitHub with Jenkins.
- Writing Jenkins pipelines using Groovy.
- Building and running Docker containers.
- Deploying a web application on AWS EC2.
- Verifying application availability using HTTP requests.

## Future Improvements

- Configure GitHub webhooks for automatic pipeline triggers.
- Add automated application tests.
- Publish Docker images to a container registry.
- Improve deployment and monitoring practices.

## Author

Tabish Mullani