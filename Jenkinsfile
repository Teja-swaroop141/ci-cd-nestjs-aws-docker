pipeline{
    agent any
    environment {
        CONTAINER_NAME= "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "steja9748@gmail.com"
        PORT = "3000"
    }

    stages{
        stage("clone repo"){
            steps{
                git branch : "main",
                url : "https://github.com/Teja-swaroop141/ci-cd-nestjs-aws-docker.git"
            }
        }


        stage("Build docker image"){
            steps{
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage("stop and remove previous container"){
            steps{
                sh '''
                   docker stop $CONTAINER_NAME || true
                   docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage("Docker container run "){
            steps{
                sh '''
                   docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage("send email Notification "){
            steps{
                emailext(
                    subject : "Nestjs app deployed on ec2 with docker ",
                    body : "your nestjs app is Deployed at http://3.26.73.86:${PORT}/",
                    to : "${EMAIL}"
                )
            }
        }


    }


}