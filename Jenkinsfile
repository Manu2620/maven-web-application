node{
  
  //echo "GitHub BranhName ${env.BRANCH_NAME}"
  //echo "Jenkins Job Number ${env.BUILD_NUMBER}"
  echo "Jenkins Node Name ${env.NODE_NAME}"
  
  echo "Jenkins Home ${env.JENKINS_HOME}"
  echo "Jenkins URL ${env.JENKINS_URL}"
  echo "JOB Name ${env.JOB_NAME}"
  
def mavenHome = tool name:"maven3.8.4"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
stage('CheckOutcode')
{
git branch: 'development', credentialsId: 'bb6f6a96-965c-4aea-af92-656a48fd987c', url: 'https://github.com/Manu2620/maven-web-application.git' 
}

stage('Build')
{
  sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport')
{
  sh "${mavenHome}/bin/mvn sonar:sonar"
}
/*stage('UploadArtifactIntoNexusRepository')
{
  sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppIntotomcatServer')
{
   sshagent(['be6e4fad-34a1-4f23-aad2-7ee1ac7fec89']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.51.161:/opt/apache-tomcat-9.0.58/webapps/"
}
}
/*stage('SendEmailNotification'){
mail bcc: '', body: '''Build Over
 
Regards,
Manorama Shevale
7387791049''', cc: 'manoramashevale@gmail.com', from: '', replyTo: '', subject: 'Build Over!!!', to: 'manoramashevale@gmail.com'
}*/
}
