pipeline {
    agent any

    environment {
        APP = "home-dashboard"
    }

    stages {
        stage("Stop and Delete container") {
            steps {
                script {
                    sh "docker stop \$(docker container ls -a -q --filter ancestor=${APP})"
                    sh "docker rm \$(docker container ls -a -q --filter ancestor=${APP})"
                    sh "docker rmi \$(docker images -a -q ${APP})"
                }
            }
        }
        stage("Build") {
            steps {
                script {                
                    sh "docker build -t ${APP} ."
                }
            }
        }
        stage("Deploy") {
            steps {
                script {
                    sh "docker run -p 80:80 -d ${APP}"
                }
            }
        }
    }    
}