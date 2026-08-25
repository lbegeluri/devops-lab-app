pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE = "levanietuna5/devops-lab-app"
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }
        stage('Push') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push $IMAGE:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
