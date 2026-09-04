pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                dir('/home/ubuntu/Jenkins_Solution_frontend') {
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('/home/ubuntu/Jenkins_Solution_frontend') {
                    sh '''
                        npm ci
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                dir('/home/ubuntu/Jenkins_Solution_frontend') {
                    sh '''
                        node --check app.js
                    '''
                }
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
