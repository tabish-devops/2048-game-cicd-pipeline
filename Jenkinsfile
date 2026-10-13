
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'shopsphere-2048'
        CONTAINER_NAME = 'shopsphere-2048'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is available in the workspace.'
                sh 'ls -la app'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} app'
                sh 'docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker image inspect ${IMAGE_NAME}:latest'
            }
        }

        stage('Deploy Locally') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d \
                      --name ${CONTAINER_NAME} \
                      -p 8081:80 \
                      ${IMAGE_NAME}:latest
                '''
            }
        }

        
    }

    post {
        success {
            echo 'Pipeline successful. Open http://localhost:8081'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs in Jenkins.'
        }
    }
}
