pipeline {
    agent any

    environment {
        MINIKUBE_HOME = 'C:\\Users\\jonna\\.minikube'
        KUBECONFIG = 'C:\\Users\\jonna\\.kube\\config'
        HOME = 'C:\\Users\\jonna'
        USERPROFILE = 'C:\\Users\\jonna'

        DOCKER_IMAGE = 'devops-website:latest'
        K8S_DEPLOYMENT = 'devops-flow'
        K8S_SERVICE = 'devops-flow-service'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                git branch: 'main',
                    url: 'https://github.com/vinayjonnadula11-svg/devops-website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Check Minikube Access') {
            steps {
                echo 'Checking Minikube profile'
                bat 'whoami'
                bat 'echo MINIKUBE_HOME=%MINIKUBE_HOME%'
                bat 'minikube -p minikube profile list'
                bat 'kubectl config current-context'
            }
        }

        stage('Load Image into Minikube') {
            steps {
                echo 'Loading Docker image into Minikube'
                bat 'minikube -p minikube image load %DOCKER_IMAGE%'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Applying Kubernetes deployment and service'
                bat 'kubectl apply -f k8s/'
            }
        }

        stage('Restart Deployment') {
            steps {
                echo 'Restarting Kubernetes deployment'
                bat 'kubectl rollout restart deployment/%K8S_DEPLOYMENT%'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Waiting for deployment rollout'
                bat 'kubectl rollout status deployment/%K8S_DEPLOYMENT% --timeout=180s'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the Console Output for the failed stage.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}