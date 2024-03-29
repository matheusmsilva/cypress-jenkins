pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {

        stage('Downloading dependencies') {
            steps {
                bat "npm i"
            }
        }

        stage('Testing with chrome') {
            steps {
                bat "npx cypress run --browser chrome"
            }
        }

        stage('Testing with edge') {
            steps {
                bat "npx cypress run --browser edge"
            }
        }

         stage('Testing with edge') {
            steps {
                echo "Deploying"
            }
        }
    }


    post {
        always {            
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: 'Example title'])
        }
    }
}