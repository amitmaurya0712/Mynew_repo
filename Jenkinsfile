pipeline{
    agent any
    environment {
        AWS_ACCOUNT_ID = "964715276857"
        AWS_REGION = "us-west-2"
        IMAGE_REPO_NAME = "jenkins_push"
        IMAGE_TAG = "latest"
        REPOSITORY_URL = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
    stages{
        stage("AWS ECR"){
            steps{
                script{
                    sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
                }
            }
        }
        
        stage("Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/amitmaurya0712/Mynew_repo.git'
            }
        }

        stage("Docker BUILD"){
            steps{
                script{
                    dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage("Pushing Image to ECR"){
            steps{
                script{
                    sh "docker tag jenkins_push:latest 964715276857.dkr.ecr.us-west-2.amazonaws.com/jenkins_push:latest" 
                    sh "docker push 964715276857.dkr.ecr.us-west-2.amazonaws.com/jenkins_push:latest"
                }
            }

        }
    }
        post {
        success {
            emailext (
                subject: 'Docker image pushed to ECR',
                body: 'The Docker image was successfully pushed to ECR.',
                to: 'amit.maurya@xenonstack.com',
                mimeType: 'text/html',
                attachLog: true,
                compressLog: true,
                replyTo: 'amit.maurya@xenonstack.com',
                from: 'amit.maurya@xenonstack.com'
            )
        }
    }
}

