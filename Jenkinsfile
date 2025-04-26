pipeline {
    agent any

    environment {
        IMAGE_NAME = 'esha01/flash-docker-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Ritiksharma0004/Node_JS-Application'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: '76fe76f9-8675-41e8-980c-436ca810d094',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', '76fe76f9-8675-41e8-980c-436ca810d094') {
                            docker.image("${IMAGE_NAME}").push('latest')
                        }
                    }
                }
            }
        }
    }
}
