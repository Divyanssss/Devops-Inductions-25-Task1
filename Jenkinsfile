pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "divyanshjoshi"
        DOCKERHUB_PAT  = credentials('dockerpass')
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
                    bat "docker build -t %DOCKERHUB_USER%/devops-inductions-25-task1-frontend ."
                    bat "echo %DOCKERHUB_USER%:%DOCKERHUB_PAT% | docker login --username %DOCKERHUB_USER% --password-stdin"
                    bat "docker push %DOCKERHUB_USER%/devops-inductions-25-task1-frontend"
                }
            }
        }

        stage('Build & Push Backend') {
            steps {
                dir('Backend') {
                    bat "docker build -t %DOCKERHUB_USER%/devops-inductions-25-task1-backend ."
                    bat "echo %DOCKERHUB_USER%:%DOCKERHUB_PAT% | docker login --username %DOCKERHUB_USER% --password-stdin"
                    bat "docker push %DOCKERHUB_USER%/devops-inductions-25-task1-backend"
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
