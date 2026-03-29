pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "abhijeet12345678/devops-app"
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Abhijeet-Mohite/java-devops-app.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }
}