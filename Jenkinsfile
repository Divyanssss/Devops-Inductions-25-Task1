pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "divyanshjoshi"
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

        stage('Test Backend') {
            steps { 
                dir('Backend') {
                    bat 'cargo test'
                }
            }
        }

        stage('Build & Push Frontend') {
            steps {
                script {
                    dir('Frontend') {
                        bat "docker build -t %DOCKERHUB_USER%/devops-inductions-25-task1-frontend ."
                        
                        withCredentials([string(credentialsId: 'dockerpass', variable: 'DOCKER_PAT')]) {
                            bat 'echo %DOCKER_PAT% | docker login -u %DOCKERHUB_USER% --password-stdin'
                        }
                        
                        bat "docker push %DOCKERHUB_USER%/devops-inductions-25-task1-frontend"
                    }
                }
            }
        }

        stage('Build & Push Backend') {
            steps {
                script {
                    dir('Backend') {
                        bat "docker build -t %DOCKERHUB_USER%/devops-inductions-25-task1-backend ."
                        
                        withCredentials([string(credentialsId: 'dockerpass', variable: 'DOCKER_PAT')]) {
                            bat 'echo %DOCKER_PAT% | docker login -u %DOCKERHUB_USER% --password-stdin'
                        }
                        
                        bat "docker push %DOCKERHUB_USER%/devops-inductions-25-task1-backend"
                    }
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
