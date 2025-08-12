pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Sreeya-Vadakattu/Devops-node-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('sreeyav/devops-node-app')
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    script {
                        docker.image('sreeyav/devops-node-app').push('latest')
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
