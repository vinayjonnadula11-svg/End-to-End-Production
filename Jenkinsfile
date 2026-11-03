pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Getting source code from GitHub'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building website Docker image'
                bat 'docker build -t devops-website:latest .'
            }
        }
        stage('Check Jenkins Environment') {
    steps {
        bat 'whoami'
        bat 'minikube profile list'
        bat 'kubectl config current-context'
        bat 'docker context show'
    }
}

        stage('Load Image into Minikube') {
            steps {
                echo 'Loading Docker image into Minikube'
                bat 'minikube image load devops-website:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Applying Kubernetes configuration'
                bat 'kubectl apply -f k8s/'
            }
        }

        stage('Restart Deployment') {
            steps {
                echo 'Restarting website deployment'
                bat 'kubectl rollout restart deployment/devops-flow'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Waiting for deployment to become ready'
                bat 'kubectl rollout status deployment/devops-flow --timeout=120s'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }

    post {
        success {
            echo 'Website deployed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the Console Output for errors.'
        }
    }
}