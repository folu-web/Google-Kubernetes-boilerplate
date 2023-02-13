pipeline {
    agent any
    
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t frontend .'
            }
        }
        
        stage('Test') {
            steps {
                sh 'docker run -d -p frontend frontend'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh 'docker login -u folumii -p dckr_pat_3htEwdzErAa3N4Doxkyo_XcBx6k'
                sh 'docker push frontend'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f <kubernetes-manifest-file>.yml'
            }
        }
    }
}
