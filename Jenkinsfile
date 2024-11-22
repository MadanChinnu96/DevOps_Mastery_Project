pipeline {
    agent any

    environment {
        // Any environment variables you might need
        DOCKER_IMAGE = 'madanchinnu/my-docker-image'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    // You can build your docker image or any other build commands here
                    sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Run your tests here
                    sh 'pytest tests/test_app.py'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying application...'
                    // Deploy your app or run docker commands here
                    sh 'docker run -d -p 5000:5000 --name sample-app-container ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Clean up resources here (e.g., stop containers)
            sh 'docker stop sample-app-container || true'
            sh 'docker rm sample-app-container || true'
        }
    }
}

