pipeline {
    agent any
    environment {
        def app
        def appName = "jmgross.dev"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                app = docker.build("jimmacle/${appName}")
            }
        }
        stage('Deploy') {
            steps {
                sh "docker stop ${appName} || true"
                sh "docker rm ${appName} || true"
                app.run("-d --name ${appName} --network proxy")
            }
        }
    }
}