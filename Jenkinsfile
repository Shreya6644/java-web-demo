pipeline{
echo "The node name is: ${env.NODE_NAME} "
echo "The build number is: ${env.BUILD_NUMBER} "
agent any
tools{
 maven 'maven3.9.6'
}
stages{
 stage('CodeCheckout'){
  steps{
   git branch:'main',credentialsId:'5fb3a952-01fc-4a08-930a-3691be4d5c09',url:'https://github.com/Shreya6644/java-web-demo.git'
  }
 }
 stage('Build'){
  steps{
   sh "mvn clean package"
  }
 }
 stage('ExecuteSonarqubeReport'){
  steps{
   sh "mvn sonar:sonar"
  }
 }
 stage('UploadArtifactIntoNexus'){
  steps{
   sh "mvn deploy"
  }
 }
 stage('DeployToTomacat'){
  steps{
   sshagent(['774f3525-0899-4571-bf73-3e2562f1dbbc']) {
    sh "scp -o StrictHostKeyChecking=no target/java-web-demo.war ec2-user@98.130.122.77:/opt/tomcat9/webapps"
  }
 }
 }
}
}
