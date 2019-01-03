pipeline {
  agent { label 'docker-agent' }
  stages {
    stage('Build') {
      steps {
        git url: 'https://github.com/sunilmbhoi/docker.git'
        sh 'curl -O -v http://192.168.56.1:8081/repository/jenkinsartifacts/sampleweb.war'
        sh 'docker build -t samplweb:${BUILD_NUMBER} . '
        sh 'docker tag samplweb:${BUILD_NUMBER} 192.168.56.1:5000/samplweb:${BUILD_NUMBER}'
        sh 'docker push 192.168.56.1:5000/samplweb:${BUILD_NUMBER}'
      }
    }
    stage('Preparation') {
      steps { 
    //Installing kubectl in Jenkins agent
        sh 'curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl'
        sh 'chmod +x ./kubectl && mv kubectl /usr/sbin'

        //Clone git repository
        git url:'https://github.com/sunilmbhoi/k8s.git'
      }
  }

     stage('Integration') {
       steps { 
         sh "sed -i 's/imagename:tag/samplweb:${BUILD_NUMBER}/g' deploy/sample-deployment.yaml"
         withKubeConfig([credentialsId: 'jenkins-deployer-credentials', serverUrl: 'https://192.168.56.191:6443']) {
         sh 'kubectl apply -f deploy/ --namespace=default'
           
         }
    }
  }

  }
}
