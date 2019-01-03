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
  }
}
