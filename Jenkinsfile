import groovy.json.JsonOutput

def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger'
]

def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

pipeline {
    agent any

    environment {
        BUILD_USER = ''
    }
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

        stage('Deploy') {
            steps {
                echo "Deploying"
            }
        }
    }


    post {
        always {   

            script {
                BUILD_USER = getBuildUser()
            }

            slackSend channel: '#jenkins-example',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${BUILD_USER}\n More info at: ${env.BUILD_URL}HTML_20Report/"

            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: 'Example title'])
        }
    }
}