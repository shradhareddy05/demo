pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'docker build -t bootstrap-site .'
            }
        }
        stage('Deploy') {
            steps {
                bat '''
                docker stop bootstrap-container || exit 0
                docker rm bootstrap-container || exit 0
                docker run -d --name bootstrap-container -p 8081:80 bootstrap-site
                '''
            }
        }
    }
}
