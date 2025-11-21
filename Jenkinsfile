pipeline{
  agent any
  tools {
    maven  'Maven-3.9.9'
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
      post{
        success{
          echo "Archiving the Artifacts"
          archiveArtifacts artifacts:'**/target/*.war'
        }
      }
    }
    stage('Deploy to tomcat server') {
          steps{
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat-deploy', path: '', url: 'http://34.217.5.184:8080/')], contextPath: null, war: '**/*.war'
          }
   }    
  }         
}
