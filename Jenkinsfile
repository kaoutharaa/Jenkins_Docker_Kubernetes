pipeline {
    agent any
    environment {
        IMAGE_NAME = 'devops-demo'
    }
    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Run Container') {
            steps {
                sh '''
                docker rm -f $IMAGE_NAME || true
                docker run -d \
                    -p 8080:8080 \
                    -p 50000:50000 \
                    -v jenkins_home:/var/jenkins_home \
                    -v /var/run/docker.sock:/var/run/docker.sock \
                    --name $IMAGE_NAME \
                    $IMAGE_NAME
                '''
            }
        }
    }
}