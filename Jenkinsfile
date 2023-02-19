pipeline {
  agent any
  stages {
    stage ('Testing') {
      steps {
          git branch: 'main', credentialsId: 'for-git', url: 'https://github.com/folu-web/google-Kubernetes-boilerplate.git'
          sh ''' sudo docker system prune -af
                  '''
           sh ''' cd app/adservice
                   ls -la
                   sudo docker --version
                   sudo docker build -t folumii/adservice .
                   sudo docker login -u folumii -p dckr_pat_3htEwdzErAa3N4Doxkyo_XcBx6k
                   sudo docker push folumii/adservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' cd app/frontend
                   ls
                   sudo docker build -t folumii/frontend .
                   sudo docker push folumii/frontend
                   '''
         sh ''' sudo docker system prune -af
                  '''
        
         sh '''    cd app/cartservice/src
                   ls
                   sudo docker build -t folumii/cartservice .
                   sudo docker push folumii/cartservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' cd app/checkoutservice
                   ls
                   sudo docker build -t folumii/checkoutservice .
                   sudo docker push folumii/checkoutservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' cd app/currencyservice
                   ls
                   sudo docker build -t folumii/currencyservice .
                   sudo docker push folumii/currencyservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' cd app/emailservice
                   ls
                   sudo docker build -t folumii/emailservice .
                   sudo docker push folumii/emailservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' cd app/loadgenerator
                   ls
                   sudo docker build -t folumii/loadgenerator .
                   sudo docker push folumii/loadgenerator
                   '''
         sh ''' sudo docker system prune -af
                  '''
         sh ''' cd app/paymentservice
                   ls
                   sudo docker build -t folumii/paymentservice .
                   sudo docker push folumii/paymentservice
                   '''
        sh ''' sudo docker system prune -af
                 '''
        sh ''' cd app/productcatalogservice
                  ls
                  sudo docker build -t folumii/productcatalogservice .
                  sudo docker push folumii/productcatalogservice
                  '''
         sh ''' sudo docker system prune -af
                 '''
        sh ''' cd app/recommendationservice
                  ls
                  sudo docker build -t folumii/recommendationservice .
                  sudo docker push folumii/recommendationservice
                  '''
         sh ''' sudo docker system prune -af
                 '''
        sh ''' cd app/shippingservice
                  ls
                  sudo docker build -t folumii/shippingservice .
                  sudo docker push folumii/shippingservice
                  '''
        
      }
    }
     stage ('Create Deploy to Yaml file') {
       steps {
           withCredentials([aws(credentialsId: 'aws-credentials', region: 'ca-central-1')]) {
           sh 'kubectl version --client --output=yaml'
           sh '''
                 aws eks update-kubeconfig --name bootdemo
                 kubectl config current-context
                 kubectl config use-context arn:aws:eks:ca-central-1:487585538889:cluster/bootdemo
                 kubectl apply -f testing.yaml
                 kubectl get service
                 '''
           }
         }
       }
  }
}
