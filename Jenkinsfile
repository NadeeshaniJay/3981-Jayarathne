pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/NadeeshaniJay/3981-Jayarathne.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t nadeeshanijay/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'nadeeshani-docker', variable: 'nadeeshanidocker')]) {
   
               bat'docker login -u nadeeshanijay -p ${nadeeshanidocker}'
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push nadeeshanijay/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}