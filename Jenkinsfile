pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "abhijeet12345678/devops-app"
    }

    options {
        // This will wipe out the workspace at the start of the build
        wipeWorkspace()
        // Keep build logs for 10 builds
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Clean Workspace') {
            steps {
                echo 'Cleaning workspace...'
                deleteDir() // deletes all files in current workspace
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