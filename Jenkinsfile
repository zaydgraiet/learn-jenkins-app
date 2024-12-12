pipeline {
    agent any
    environment {
        DOCKER_HOST = '' // Unset DOCKER_HOST to avoid issues
        DOCKER_USERNAME = 'your-docker-username' // Provide your Docker username
        DOCKER_PASSWORD = 'your-docker-password' // Provide your Docker password
    }
    stages {
        stage('Docker Login') {
            steps {
                script {
                    // If you need to login to Docker registry
                    sh '''
                    echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                    '''
                }
            }
        }

        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine' // Docker image
                    reuseNode true
                }
            }
            steps {
                sh '''
                echo "Listing files in the workspace:"
                ls -la
                echo "Node.js version:"
                node --version
                echo "NPM version:"
                npm --version
                echo "Installing dependencies..."
                npm ci
                echo "Building the project..."
                npm run build
                echo "Files after build:"
                ls -la
                '''
            }
        }
    }
}
