pipeline {
    agent any

    environment {
       DOCKERHUB_CREDS = credentials('dockerhub-creds')
       DOCKERHUB_USER = DOCKERHUB_CREDS.username
       DOCKERHUB_PASS = DOCKERHUB_CREDS.password
    }

    stages {
        stage('get code') {
            steps {
                git branch: 'main', url: 'https://github.com/Divyanssss/Devops-Inductions-25-Task1.git'

            }
        }

        stage('Test Frontend') {
            steps {
                dir('Frontend') {
                    bat 'npm install'
                    bat 'npm test'
                }
            }
        }

        stage('Build & Push Frontend') {
            steps {
                dir('Frontend') {
                    bat 'docker build -t %DOCKERHUB_USER%/devops-inductions-25-task1-frontend .'
                    bat 'echo %DOCKERHUB_PASS% | docker login -u %DOCKERHUB_USER% --password-stdin'
                    bat 'docker push %DOCKERHUB_USER%/devops-inductions-25-task1-frontend'
                }
            }
        }

        stage('Build & Push Backend') {
            steps {
                dir('Backend') {
                    bat 'docker build -t %DOCKERHUB_USER%/devops-inductions-25-task1-backend .'
                    bat 'echo %DOCKERHUB_PASS% | docker login -u %DOCKERHUB_USER% --password-stdin'
                    bat 'docker push %DOCKERHUB_USER%/devops-inductions-25-task1-backend'
                }
            }
        }

        stage('Docker Compose') {
            steps {
                bat 'docker compose down || true'
                bat 'docker compose up -d --build'
            }
        }
    }
}
