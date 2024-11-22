pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = "hello-app"
        DOCKER_PORT = '3000'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out the code from SCM..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker container..."
                sh """
                docker run -d -p ${DOCKER_PORT}:${DOCKER_PORT} --name ${DOCKER_IMAGE} ${DOCKER_IMAGE}
                """
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed. Check the logs for errors."
        }
    }
}
