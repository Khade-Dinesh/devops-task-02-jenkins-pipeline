
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'dineshkhade/nodejs-demo-app'
        CONTAINER_NAME = 'nodejs-demo-app'
        APP_PORT = '3000'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Node.js application...'
                dir('app') {
                    sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running application tests inside Docker...'
                dir('app') {
                    sh '''
                        docker run --rm \
                          -v "$PWD:/app" \
                          -w /app \
                          node:22-alpine npm ci
                    '''

                    sh '''
                        docker run --rm \
                          -v "$PWD:/app" \
                          -w /app \
                          node:22-alpine npm test
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application with Docker...'
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true

                    docker run -d \
                      --name ${CONTAINER_NAME} \
                      --restart unless-stopped \
                      -p ${APP_PORT}:3000 \
                      ${IMAGE_NAME}:${BUILD_NUMBER}
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs.'
        }
    }
}

