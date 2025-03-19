pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            args '-v jenkins-npm-cache:/root/.npm'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                echo 'Building the application...'
                ls -la
                node -v
                npm -v
                npm ci
                npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                echo 'Running the tests...'
                npm run test
                '''
            }
        }
    }
}

