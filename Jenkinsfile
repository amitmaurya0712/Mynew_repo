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
                    sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URL}:${IMAGE_TAG}" 
                    sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/jenkins_push:${IMAGE_TAG}"
                }
            }

        }

    }
}
