pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'node:18-alpine' // Docker image
    }
    stages {
        stage('Docker Login') {
            steps {
                script {
                    // Using Jenkins credentials (replace 'docker-credentials' with your Jenkins credentials ID)
                    withCredentials([usernamePassword(credentialsId: 'zaydgraiet', usernameVariable: 'Graiet', passwordVariable: 'admin')]) {
                        // Perform Docker login using the credentials
                        sh '''
                        echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                        '''
                    }
                }
            }
        }

        stage('Build') {
            agent {
                docker {
                    image "${DOCKER_IMAGE}" // Use Docker image
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
