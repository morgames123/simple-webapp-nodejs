pipeline {
    agent any
    
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    
    triggers {
        cron('H */4 * * 1-5')
    }

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
                script {
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
