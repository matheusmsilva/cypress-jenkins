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
        
        stage('Deploy'){
            steps {
                echo "Deploying"
            }
        }
    }
}