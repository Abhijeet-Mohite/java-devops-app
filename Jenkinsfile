pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "abhijeet12345678/devops-app"
    }

    options {
        // Keep build logs for 10 builds
        buildDiscarder(logRotator(numToKeepStr: '10'))
        // Optional: timestamps in console
        timestamps()
    }

    stages {
        stage('Clean Workspace') {
            steps {
                echo 'Cleaning workspace...'
                deleteDir() // deletes everything in current workspace
            }
        }

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Abhijeet-Mohite/java-devops-app.git'
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

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check console output.'
        }
    }
}