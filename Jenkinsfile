pipeline {
  agent any
  stages {
    
    stage('Scan') {
      steps{
        ([$class: 'CxScanBuilder', comment: '', credentialsId: '', dependencyScanConfig: [dependencyScanExcludeFolders: '', dependencyScanPatterns: '', fsaVariables: '', osaArchiveIncludePatterns: '*.zip, *.war, *.ear, *.tgz', scaAccessControlUrl: 'https://platform.checkmarx.net', scaCredentialsId: '', scaServerUrl: 'https://api-sca.checkmarx.net', scaTenant: '', scaWebAppUrl: 'https://sca.checkmarx.net'], excludeFolders: '', exclusionsSetting: 'global', failBuildOnNewResults: false, failBuildOnNewSeverity: 'HIGH', filterPattern: '', fullScanCycle: 10, password: '{AQAAABAAAAAQzsAIQuZtfXRiBgQWUsqs7NpbUomtj4Ee/rYzo87WZkU=}', projectName: 'checkmarx', sastEnabled: true, serverUrl: '', sourceEncoding: 'Provide Checkmarx server credentials to see source encodings list', username: 'rod', vulnerabilityThresholdResult: 'FAILURE', waitForResultsEnabled: true])
      }
    }
    
    stage('Build') {
      steps { 
        sh 'cd ~/workspace/AKS/ && terraform apply -auto-approve && sleep 1m' 
      }
    }
    
    stage('Update') {
      steps { 
        sh 'rm -rf ~/.kube/config && az aks get-credentials --resource-group aks-cluster --name aks && sleep 1m' 
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
        sh 'cd ~/workspace/AKS/ && sleep 4m && kubectl get svc'
      }
    }
  }
}
