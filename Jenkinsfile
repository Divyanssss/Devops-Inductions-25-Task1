pipeline {
    agent any

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
                    withCredentials([usernamePassword(credentialsId: '836e34ec-6d9e-463e-b8c1-fc16ee6f8bc9', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        bat 'docker build -t %DOCKER_USER%/devops-inductions-25-task1-frontend .'
                        bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                        bat 'docker push %DOCKER_USER%/devops-inductions-25-task1-frontend'
                    }
                }
            }
        }

        stage('Build & Push Backend') {
            steps {
                dir('Backend') {
                    withCredentials([usernamePassword(credentialsId: '836e34ec-6d9e-463e-b8c1-fc16ee6f8bc9', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        bat 'docker build -t %DOCKER_USER%/devops-inductions-25-task1-backend .'
                        bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                        bat 'docker push %DOCKER_USER%/devops-inductions-25-task1-backend'
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
