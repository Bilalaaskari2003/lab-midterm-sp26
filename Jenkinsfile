pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Bilalaaskari2003/lab-midterm-sp26.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt --break-system-packages'
            }
        }

        stage('Train Model') {
            steps {
                sh 'python3 train.py'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop ml-api-container || true'
                sh 'docker rm ml-api-container || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ml-api .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8000:8000 --name ml-api-container ml-api'
            }
        }
    }
}
