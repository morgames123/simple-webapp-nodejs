@Library("jenkinsLib@main") _

pipeline {
    agent any

    stages {
        stage("Clean Workspace") {
            steps {
                cleanWs()
                runCommand()
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
                script {
                    config = readYaml(text: libraryResource("environment.yml"))
                    print (config.buildImage)
                    try {
                        sh "docker rm --force nodewebapp"
                    }
                    catch(all) {
                        echo "No nodewebbapp container was running"
                    }
                }
                sh "docker run -itd --name nodewebapp -p 3000:3000 nodewebapp"
                sh "docker ps"
            }
        }
    }
}
