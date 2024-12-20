pipeline {
    agent any
    
    stages {
        stage('Checkout Repository') {
            steps {
                script {
                    sh 'git clone -b main https://github.com/sophiee15/api-tests-final.git .'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t sophie14/api-tests:latest .'
                }
            }
        }
        
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    sh 'docker push sophie14/api-tests:latest'
                }
            }
        }
    }
}
