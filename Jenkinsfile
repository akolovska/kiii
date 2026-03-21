pipeline {
    agent any
    environment {
        IMAGE_NAME = "akolovska/kiii"
        DOCKERHUB_CREDENTIALS = "dockerhub"
    }
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker image') {
            steps {
                script {
                    app = docker.build("${IMAGE_NAME}:${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Push Docker image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}
