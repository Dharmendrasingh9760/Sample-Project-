pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git ''https://github.com/Dharmendrasingh9760/Sample-Project-.git
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t sample-app:latest .'
            }
        }
        stage('Push to ECR') {
            steps {
                sh './scripts/push-to-ecr.sh' // Custom script
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
