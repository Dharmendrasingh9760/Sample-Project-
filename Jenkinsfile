pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        CLUSTER_NAME = 'sample-cluster'
        IMAGE_NAME = 'sample-app'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Dharmendrasingh9760/Sample-Project-.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Deploy to EKS') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'aws-creds',
                    usernameVariable: 'AKIAR3HUOHT6ZCFQECXN',
                    passwordVariable: 'cFxZFI1HhXF4VUNxDyggvHBdzowKvnyoABVY1zZj'
                )]) {
                    sh '''
                        mkdir -p ~/.aws
                        echo "[default]" > ~/.aws/credentials
                        echo "aws_access_key_id=$AWS_ACCESS_KEY_ID" >> ~/.aws/credentials
                        echo "aws_secret_access_key=$AWS_SECRET_ACCESS_KEY" >> ~/.aws/credentials

                        aws eks update-kubeconfig --region $AWS_REGION --name $CLUSTER_NAME

                        kubectl apply -f k8s/
                    '''
                }
            }
        }
    }
}
