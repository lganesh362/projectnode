pipeline {
    agent any

    stages {
        stage('Push Docker image to ECR') {
            steps {
                script {
                    // Authenticate Docker with ECR
                    sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 130483240640.dkr.ecr.us-east-1.amazonaws.com"

                    // Build Docker image
                    sh "docker build -t ecr-image ."
//ganesh
                    // Tag Docker image
                    sh "docker tag ecr-image:latest 130483240640.dkr.ecr.us-east-1.amazonaws.com/ecr-image:latest"

                    // Push Docker image to ECR
                    sh "docker push 130483240640.dkr.ecr.us-east-1.amazonaws.com/ecr-image:latest"
                }
            }
        }

        stage('Pull Docker image from ECR') {
            steps {
                script {
                    // Pull Docker image from ECR
                    sh "docker pull 130483240640.dkr.ecr.us-east-1.amazonaws.com/ecr-image:latest"

                    // Remove existing container if it exists
                     sh 'docker container ls -a -f name=My-practice-website -q | xargs -r docker container rm -f'

                    // Run Docker container
                     sh "docker run -itd --name My-practice-website -p 3000:3000 130483240640.dkr.ecr.us-east-1.amazonaws.com/ambika-api:latest"
                        }
                    }
        }
    }
}
