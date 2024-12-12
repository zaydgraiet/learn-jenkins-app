pipeline {
    agent any
    stages {
        stage('Build') {   
            agent {        
                docker {
                    image 'node:18-alpine'
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
