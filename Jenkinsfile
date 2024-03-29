pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {
        stage('Testing') {
            steps {
                bat "npm i"
                bat "npx cypress run --browser chrome"
            }
        }
    }

    post {
        always {            
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        }
    }
}