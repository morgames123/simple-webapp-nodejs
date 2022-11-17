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
                sh "docker images"
            }
        }
        stage("Deploy") {
            steps {
                try {
                    sh "docker kill nodewebapp"
                }
                catch(all) {
                    echo "No nodewebbapp container was running
                }
                sh "docker run -itd nodewebapp --name nodewebapp -p 3000:3000"
                sh "docker ps"
            }
        }
    }
}
