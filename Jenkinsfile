// Jenkinsfile
pipeline {
    agent any

    environment {
        APP_NAME = "flask-app"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR-USERNAME/YOUR-REPO.git'
            }
        }

        stage('Verify Docker') {
            steps {
                sh 'docker version'
                sh 'docker compose version'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${APP_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Check Running Containers') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
