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
            -p 5001:5000 \
            --name $IMAGE_NAME \
            $IMAGE_NAME
        '''
    }
}
    }
}