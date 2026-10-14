
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'shopsphere-2048'
        CONTAINER_NAME = 'shopsphere-2048'
        APP_REPO = 'https://github.com/tabish-devops/2048-game.git'
        APP_PORT = '8081'
    }

    stages {
        stage('Checkout Application') {
            steps {
                sh '''
                    rm -rf app
                    git clone --depth 1 ${APP_REPO} app
                    test -f app/Dockerfile
                    ls -la app
                '''
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

        stage('Deploy Application') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d \
                      --name ${CONTAINER_NAME} \
                      --restart unless-stopped \
                      -p ${APP_PORT}:80 \
                      ${IMAGE_NAME}:latest
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh '''
                    for i in $(seq 1 15); do
                        if curl -fsS http://localhost:${APP_PORT}/ > /dev/null; then
                            echo "Application is responding successfully"
                            exit 0
                        fi
                        sleep 2
                    done

                    docker logs ${CONTAINER_NAME} || true
                    exit 1
                '''
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: CI/CD pipeline completed.'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
