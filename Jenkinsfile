pipeline {
    agent any
    environment {
        APP_NAME = "jmgross.dev"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    app = docker.build("jimmacle/${APP_NAME}")
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker stop ${APP_NAME} || true"
                sh "docker rm ${APP_NAME} || true"
                script {
                    app.run("--name ${APP_NAME} --network proxy")
                }
            }
        }
    }
}