# 2048 Game - Jenkins CI/CD Pipeline

## Project Overview

This project demonstrates a CI/CD pipeline using Jenkins, Docker, and GitHub. Jenkins pulls the application source code from GitHub, builds a Docker image, deploys the container locally, and verifies that the application is responding successfully.

## Technologies Used

- Git and GitHub
- Jenkins
- Jenkins Pipeline (Groovy)
- Docker
- Linux (Ubuntu / WSL)
- Nginx

## CI/CD Workflow

1. Checkout application code from GitHub.
2. Build a Docker image.
3. Verify the Docker image.
4. Deploy the application in a Docker container.
5. Test the application using an HTTP request.

## Project Structure

```text
2048-game-cicd-pipeline/
├── Jenkinsfile
├── README.md
└── app/
    ├── Dockerfile
    ├── LICENSE
    └── README.md
```

## Run the Application

Build the Docker image:

```bash
docker build -t shopsphere-2048:latest ./app
```

Run the container:

```bash
docker run -d --name shopsphere-2048 -p 8081:80 shopsphere-2048:latest
```

Open the application at:

http://localhost:8081

## Jenkins Pipeline

The `Jenkinsfile` defines the pipeline stages for source checkout, Docker image build, image verification, local deployment, and application health verification.

## Learning Outcomes

- Understanding CI/CD concepts.
- Automating Docker image builds.
- Deploying applications using Docker containers.
- Writing Jenkins pipelines.
- Integrating GitHub with Jenkins.

## Future Improvements

- Configure automatic builds using GitHub webhooks.
- Publish Docker images to a container registry.
- Deploy the application on AWS.
- Add automated application tests.

## Author

Tabish Mullani
