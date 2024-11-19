pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'gradle-docker-example'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Chaithu12345678/Gradle3.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests
                    sh './gradlew test'
                }
            }
        }

        stage('Run Code Coverage') {
            steps {
                script {
                    // Generate code coverage report
                    sh './gradlew jacocoTestReport'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images
            sh 'docker rmi $DOCKER_IMAGE || true'
        }
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
