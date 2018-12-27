//Jenkinsfile
node {

  stage('Preparation') {
    //Installing kubectl in Jenkins agent
    sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl'
	sh 'chmod +x ./kubectl && mv kubectl /usr/sbin'

	//Clone git repository
	git url:'https://github.com/sunilmbhoi/k8s.git'
  }

  stage('Integration') {
	
    withKubeConfig([credentialsId: 'jenkins-deployer-credentials', serverUrl: 'https://192.168.56.191']) {
      sh 'kubectl apply -f deploy/ --namespace=default'
      
    }
  }
}
