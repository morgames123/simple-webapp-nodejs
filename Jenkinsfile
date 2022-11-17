pipeline {
    agent any

    stages {
        stage("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage('Clone') {
            steps {
                git 'https://github.com/morgames123/simple-webapp-nodejs.git'
            }
        }
        stage("Build") {
            steps {
                nodejs('nodejs-8') {
                    sh 'npm install'
                }
            }
        }
        stage("Test") {
            steps {
                nodejs('nodejs-8') {
                    sh 'npm run test'
                }
            }
        }
    }
    
}

