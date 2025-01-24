pipeline {
    agent any  // Run this pipeline on any available agent ex:- windows, linux, mac
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/kasun020/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps { 
                bat 'docker build -t kasun020/pipeline-tutorial-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: '', variable: 'test-pipeline')]) {
                    bat 'docker login -u kasun020 -p %test-pipeline%'
                }

            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push kasun020/pipeline-tutorial-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
