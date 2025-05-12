pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'yourdockerhubusername/my-nginx-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/docker-nginx-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t %DOCKER_IMAGE%:latest ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat "docker run -d -p 8888:80 --name jenkins-nginx %DOCKER_IMAGE%:latest"
                }
            }
        }
    }

    post {
        always { echo 'Done' }
        success { echo 'Successfully deployed!' }
        failure { echo 'Build failed' }
    }
}
