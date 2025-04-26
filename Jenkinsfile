pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creation')
        IMAGE_NAME = 'esha/flask-app'  // Your Docker Hub repo name
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/esha1401/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                bat "echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin"
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                bat "docker push %IMAGE_NAME%"
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
