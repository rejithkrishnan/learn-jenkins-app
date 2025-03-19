pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            args '-v jenkins-npm-cache:/root/.npm -v $WORKSPACE/node_modules:/app/node_modules'
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
                test -f build/index.html
                npm run test
                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
            echo 'Pipeline completed!'
        }
    }
}

