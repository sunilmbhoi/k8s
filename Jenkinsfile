//Jenkinsfile
node {
 stage('BuildingArtifact'){
  git credentialsId: 'bc045ec1-269d-465f-9164-eb103d990eaa', url: 'http://192.168.1.183:8081/NW_Pramati/sampleweb.git', branch: 'QA'
  sh 'mvn install'
  sh 'curl -v -u admin:admin123 --upload-file target/sampleweb.war http://192.168.56.1:8081/repository/jenkinsartifacts/sampleweb.war'
  }  
}
