pipeline {
    agent any
    environment {
        EKS_CLUSTER = "sample-cluster"
        REGION = "us-east-1"
    }
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Dharmendrasingh9760/Sample-Project-.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sample-app:latest .'
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh 'aws eks update-kubeconfig --region $REGION --name $EKS_CLUSTER'
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
