pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "divyanshjoshi"
        DOCKERHUB_PASS = credentials('836e34ec-6d9e-463e-b8c1-fc16ee6f8bc9') 
    }

    stages {
        stage('get code') {
            steps {
                git 'https://github.com/Divyanssss/Devops-Inductions-25-Task1.git'
            }
        }

        stage('Test Frontend') {
            steps {
                dir('Frontend') {
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        }

        stage('Build & Push Frontend') {
            steps {
                dir('Frontend') {
                    sh 'docker build -t $DOCKERHUB_USER/devops-inductions-25-task1-frontend .'
                    sh 'echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin'
                    sh 'docker push $DOCKERHUB_USER/devops-inductions-25-task1-frontend'
                }
            }
        }

        stage('Build & Push Backend') {
            steps {
                dir('Backend') {
                    sh 'docker build -t $DOCKERHUB_USER/devops-inductions-25-task1-backend .'
                    sh 'echo $DOCKERHUB_PASS | docker login -u $DOCKERHUB_USER --password-stdin'
                    sh 'docker push $DOCKERHUB_USER/devops-inductions-25-task1-backend'
                }
            }
        }

        stage('Docker Compose') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
            }
        }
    }
}
