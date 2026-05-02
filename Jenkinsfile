pipeline {
    agent any

    environment {
        IMAGE_NAME = "userna1/myapp"
    }

    stages {

        stage('Clone Source') {
            steps {
                git branch: 'main', url: 'https://github.com/TusharMgl/jenkins_lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    bat 'echo %DOCKER_TOKEN% | docker login -u userna1 --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
