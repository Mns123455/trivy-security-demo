
pipeline {
    agent any

    environment {
        TRIVY = 'C:\\Users\\K.Premchand\\Downloads\\trivy_0.76.2_windows-64bit\\trivy.exe'
    }

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
                bat '"%TRIVY%" fs --severity HIGH,CRITICAL .'
            }
        }

        stage('Trivy Docker Image Scan') {
            steps {
                bat '"%TRIVY%" image --severity HIGH,CRITICAL trivy-security-demo:v1'
            }
        }

        stage('Trivy Kubernetes Scan') {
            steps {
                bat '"%TRIVY%" config --severity HIGH,CRITICAL k8s'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s\\'
            }
        }
    }
}
