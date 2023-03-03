pipeline {
    agent {
        docker {
            image 'node:14.4-alpine3.11' 
            args '-p 3000:3000 -u 0:0' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'node --version'
                sh 'npm --version'
                sh 'npm ci'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test --coverage --watchAll=false'
            }
        }
    }
}
