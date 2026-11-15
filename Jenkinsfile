pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps { checkout scm }
        }
        stage('Test') {
            steps {
                sh '''
                pip3 install flask --break-system-packages
                python3 -m unittest discover -s .
                '''
            }
        }
        stage ('Build Docker Image') {
            steps { sh 'docker build -t devops-mini-app:latest .' }
        }
        stage('Deploy Container') {
            steps {
                sh 'docker rm -f mini-app || true'
                sh 'docker run -d -p 8085:5000 --name mini-app devops-mini-app:latest'
            }
        }
    }
}
