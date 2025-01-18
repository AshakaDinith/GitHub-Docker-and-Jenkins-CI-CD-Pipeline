pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/AshakaDinith/GitHub-Docker-and-Jenkins-CI-CD-Pipeline'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t ashaka99/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhub-pass')]) {
                script {
                            bat "docker login -u ashaka99 -p %test-dockerhub-pass%"
                        }
            }
               }
        }
        stage('Push Image') {
            steps {
                bat 'docker push ashaka99/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
