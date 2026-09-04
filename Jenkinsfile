pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    npm ci
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    node --check app.js
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    sudo systemctl restart express-frontend
                    sudo systemctl is-active --quiet express-frontend
                '''
            }
        }
    }

    post {
        success {
            echo 'Express frontend deployed successfully!'
        }

        failure {
            echo 'Express frontend deployment failed!'
        }
    }
}