
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

        stage('Verify Application') {
            steps {
                sh '''
                    for i in $(seq 1 15); do
                      if curl -fsS http://localhost:8081/ > /dev/null; then
                        echo "2048 game is responding successfully."
                        exit 0
                      fi
                      sleep 2
                    done
                    echo "Application health check failed."
                    docker logs ${CONTAINER_NAME} || true
                    exit 1
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
