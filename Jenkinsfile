pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t registration-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                    docker stop registration-app
                    docker rm registration-app
                    docker run -d --name registration-app -p 5001:5000 registration-app
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }

        failure {
            echo 'Build or deployment failed!'
        }
    }
}
