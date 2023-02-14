pipeline {
    agent { label 'slave'} 
    stages {
       stage('ECR login') {
            steps {
                script{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 677538114768.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
       }
         stage('Creating Image') {
            steps {
                script{
                sh 'echo FROM httpd:2.4 >> Dockerfile'
                }
            }
        }
         stage('Build and tag image') {
            steps {
                script{
                sh ''' docker build -t task .
                docker images
                docker tag task:latest 677538114768.dkr.ecr.us-east-1.amazonaws.com/task:latest'''
                }
            }
        }
         stage('Push and pullimage ') {
            steps {
                script{
                  sh 'docker push 677538114768.dkr.ecr.us-east-1.amazonaws.com/task:latest'
                  sh 'docker pull 677538114768.dkr.ecr.us-east-1.amazonaws.com/task:latest'
                  sh 'docker images'
                  sh 'docker run -td --name mycontainer${BUILD_NUMBER} 677538114768.dkr.ecr.us-east-1.amazonaws.com/task:latest'
                 
                }
            }
        }

    }
}
    
