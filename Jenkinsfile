pipeline {
    agent any
    
    stages {
        stage('Gitclone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: 'for-git', url: 'https://github.com/folu-web/Google-Kubernetes-boilerplate.git'
                sh 'pwd'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker --version'
                sh 'cd Google-Kubernetes-boilerplate'
                sh 'sudo docker build -t adservice .'
                sh 'ls'
                sh 'docker images'
                
            }
        }
        
        stage('Test') {
            steps {
                sh 'sudo docker run --name adservice -d -p 7700:9555 adservice'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh 'docker login -u folumii -p dckr_pat_3htEwdzErAa3N4Doxkyo_XcBx6k'
                sh 'docker push frontend2'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f <kubernetes-manifest-file>.yml'
            }
        }
    }
}
