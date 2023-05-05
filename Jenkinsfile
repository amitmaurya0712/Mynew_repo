pipeline{
    agent any
    environment {
        AWS_ACCOUNT_ID = "964715276857"
        AWS_REGION = "us-west-2"
        IMAGE_REPO_NAME = "jenkins_push"
        IMAGE_TAG = "latest"
        REPOSITORY_URL = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/{IMAGE_REPO_NAME}"
    }
    stages{
        stage("AWS ECR"){
            steps{
                script {
                    sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.comaws ecr get-login-password --region ${AWS_REGION}"
                }
            }
        }

        stage("Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/amitmaurya0712/Mynew_repo.git'
            }
        }
    }
}
