//Jenkinsfile
pipeline {
stages {
 stage('BuildingArtifact'){
  steps{
  git credentialsId: 'bc045ec1-269d-465f-9164-eb103d990eaa', url: 'http://192.168.1.183:8081/NW_Pramati/sampleweb.git', branch: 'QA'
  sh 'mvn install'
  sh 'curl -v -u admin:admin123 --upload-file target/sampleweb.war http://192.168.56.1:8081/repository/jenkinsartifacts/sampleweb.war'
  }
 }  
 stage('BuildImage'){
  steps {
    agent { label 'docker-agent' }
    git url: 'https://github.com/sunilmbhoi/docker.git'
    sh 'curl -O -v http://192.168.56.1:8081/repository/jenkinsartifacts/sampleweb.war'
    sh 'docker build -t samplweb:${BUILD_NUMBER} . '
    sh 'docker tag samplweb:${BUILD_NUMBER} 192.168.56.1:5000/samplweb:${BUILD_NUMBER}'
    sh 'docker push 192.168.56.1:5000/samplweb:${BUILD_NUMBER}'
 }
 }
}
}
