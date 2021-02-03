pipeline {
  agent any
  stages {
   
    stage('Build') {
      steps { 
        sh 'cd ~/workspace/AKS/ && terraform apply -auto-approve && sleep 2m' 
      }
    }
    
    stage('Update') {
      steps { 
        sh 'cd ~/workspace/AKS/ && az aks get-credentials --resource-group aks-cluster --name aks && sleep 2m' 
      }
    }
    
    stage('Provision') {
      steps { 
        sh 'cd ~/workspace/AKS/ && kubectl create deployment unit1 --image=nextcloud:latest --port=80'
      }
    }
    
    stage('Expose') {
      steps { 
        sh 'cd ~/workspace/AKS/ && kubectl expose deployment unit1 --type=LoadBalancer --port=3000 --target-port=80'
      }
    }
    
    stage('Return') {
      steps { 
        sh 'cd ~/workspace/AKS/ && kubectl get svc'
      }
    }
    
  }
}
