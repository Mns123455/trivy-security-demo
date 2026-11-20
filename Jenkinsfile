
pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t trivy-security-demo:v1 .'
            }
        }

        stage('Trivy Filesystem Scan') {
            steps {
                bat 'trivy.exe fs --severity HIGH,CRITICAL .'
            }
        }

        stage('Trivy Docker Image Scan') {
            steps {
                bat 'trivy.exe image --severity HIGH,CRITICAL trivy-security-demo:v1'
            }
        }

        stage('Trivy Kubernetes Scan') {
            steps {
                bat 'trivy.exe config --severity HIGH,CRITICAL k8s'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s\\'
            }
        }
    }
}
