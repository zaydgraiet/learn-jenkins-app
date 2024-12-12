pipeline {
    agent any
    environment {
        DOCKER_HOST = '' // You can also unset it like this globally, if needed
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Unset DOCKER_HOST before running docker commands
                    sh 'unset DOCKER_HOST'
                    
                    // Now you can run your Docker commands
                    sh 'docker login $CI_REGISTRY -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD'
                    sh 'docker pull node:18-alpine'
                    // Add other Docker-related commands as needed
                }
            }
        }
    }
}
