pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/nayanahg-16/Complete-pipeline-.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t nayanahg/project3:latest .
                '''
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker push nayanahg/project3'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                microk8s.kubectl apply -f deploy.yaml
                '''
            }
        }
    }
}




