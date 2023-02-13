pipeline {
  agent any
  environment {
    CLUSTER_NAME = 'bootcamp'
    SERVICE_NAME = 'frontend'
    IMAGE_TAG = 'v1'
    K8S_NAMESPACE = 'dev'
  }
    stages {
      stage("environment preparation"){
            steps {
                sh "pwd"
                sh "ls"
                sh "echo ${USER}"
                sh "df -h"
                sh "curl ifconfig.co"
                sh "echo testing"
              sh "docker --version"
              sh "sudo docker ps"
            }
        }
      
      
    stage('Build and Push Docker Image') {
      steps {
        sh 'docker build -t frontend:$IMAGE_TAG .'
        sh 'docker push frontend:$IMAGE_TAG'
      }
    }
    stage('Deploy to EKS') {
      steps {
        withCredentials([aws(credentialsId: 'aws-credentials', region: 'ca-central-1')]) {
          sh '''
          set -e
          eval $(aws eks update-kubeconfig --name $CLUSTER_NAME)
          kubectl config use-context $CLUSTER_NAME
          kubectl -n $K8S_NAMESPACE set image deployment/$SERVICE_NAME $SERVICE_NAME=frontend:$IMAGE_TAG
          '''
        }
      }
    }
  }
}
