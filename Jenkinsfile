pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/<your-repo>/devops-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('devops-app')
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    script {
                        docker.image('devops-app').push('latest')
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
