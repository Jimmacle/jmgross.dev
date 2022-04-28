pipeline {
    agent any
    stages {
        def appName = "jmgross.dev"
        def app
        stage('Checkout') {
            checkout scm
        }
        stage('Build') {
            app = docker.build("jimmacle/${appName}")
        }
        stage('Deploy') {
            sh "docker stop ${appName} || true"
            sh "docker rm ${appName} || true"
            app.run("-d --name ${appName} --network proxy")
        }
    }
}