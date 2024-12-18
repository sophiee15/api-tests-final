pipeline {
    steps {
      stage('Checkout Repository') {
        steps {
          script {
            checkout scm
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
