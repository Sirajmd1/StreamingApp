pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ACCOUNT_ID = '258274811560'
        AWS_CREDS = credentials('siraj-aws-ecr-credentials')

        ECR_REPO_FRONTEND      = 'streaming-frontend'
        ECR_ADMIN_SERVICE      = 'admin-service'
        ECR_AUTH_SERVICE       = 'auth-service'
        ECR_CHAT_SERVICE       = 'chat-service'
        ECR_STREAMING_SERVICE  = 'streaming-service'
    }

    stages {

        stage('Checkout Source') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sirajmd1/StreamingApp.git'
            }
        }

        stage('ECR Login') {
            steps {
                sh '''
                aws ecr get-login-password --region ${AWS_REGION} | \
                docker login --username AWS --password-stdin \
                ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com
                '''
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh '''
                docker build -t ${ECR_REPO_FRONTEND}:latest \
                ./frontend
                '''
            }
        }

        stage('Build Admin Service Image') {
            steps {
                sh '''
                docker build -t ${ECR_ADMIN_SERVICE}:latest \
                ./backend/adminService
                '''
            }
        }

        stage('Build Auth Service Image') {
            steps {
                sh '''
                docker build -t ${ECR_AUTH_SERVICE}:latest \
                ./backend/authService
                '''
            }
        }

        stage('Build Chat Service Image') {
            steps {
                sh '''
                docker build -t ${ECR_CHAT_SERVICE}:latest \
                ./backend/chatService
                '''
            }
        }

        stage('Build Streaming Service Image') {
            steps {
                sh '''
                docker build -t ${ECR_STREAMING_SERVICE}:latest \
                ./backend/streamingService
                '''
            }
        }

        stage('Tag Images') {
            steps {
                sh '''
                docker tag ${ECR_REPO_FRONTEND}:latest \
                ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPO_FRONTEND}:latest

                docker tag ${ECR_ADMIN_SERVICE}:latest \
                ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_ADMIN_SERVICE}:latest

                docker tag ${ECR_AUTH_SERVICE}:latest \
                ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_AUTH_SERVICE}:latest

                docker tag ${ECR_CHAT_SERVICE}:latest \
                ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_CHAT_SERVICE}:latest

                docker tag ${ECR_STREAMING_SERVICE}:latest \
                ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_STREAMING_SERVICE}:latest
                '''
            }
        }

        stage('Push Images to ECR') {
            steps {
                sh '''
                docker push ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPO_FRONTEND}:latest

                docker push ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_ADMIN_SERVICE}:latest

                docker push ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_AUTH_SERVICE}:latest

                docker push ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_CHAT_SERVICE}:latest

                docker push ${ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_STREAMING_SERVICE}:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Frontend and all backend service images successfully pushed to Amazon ECR.'
        }

        failure {
            echo 'Pipeline failed. Review Jenkins console output.'
        }
    }
}
