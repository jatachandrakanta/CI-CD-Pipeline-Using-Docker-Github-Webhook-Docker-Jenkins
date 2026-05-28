pipeline{
    agent any 

    environment{
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "jatachandrakanta@gmail.com"
        PORT = "3000"
    }
    stages{
        stage("Clone Repo"){
            steps{
                git branch: "main",url:"https://github.com/jatachandrakanta/CI-CD-Pipeline-Using-Docker-Github-Webhook-Docker-Jenkins.git"
            }
        }
        stage('Build Docker Image'){
            steps{
                sh "docker build -t $IMAGE_NAME"
            }
        }
        stage('Stop & Remove Previous Container'){
            steps{
                sh '''
                    docker stop $CONTAINER_NAME 
                    || true
                    docker rm $CONTAINER_NAME || true



                '''
            }
        }
        stage('Docker Container Run'){
            steps{
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME

                '''
            }
    

    }
    stage('Send Email Notification'){
            steps{

                emailext(
                    subject: "NestJS App Deployed Succesfully on EC2!!",
                    body: "Your Nest JS app Is Deployed! http://43.205.117.53:${PORT}/",
                    to: "${EMAIL}"
                )
            }

}
    }
