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
                sh "docker build . -f Dockerfile-Shemesh -t nodewebapp"
            }
        }
    }
}
