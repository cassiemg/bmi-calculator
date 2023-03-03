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
                sh 'npm install -g jest'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test --coverage --watchAll=false'
            }
            post {
              always {
                 step([$class: 'CoberturaPublisher', autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'output/coverage/jest/cobertura-coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false])
              }
            }
        }
    }
}
