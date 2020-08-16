node
 {
 
 def mavenHome = tool name: "maven-3.6.3"
 
  /* properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
*/ 
 stage('CheckoutCode')
 {
 git url: 'https://github.com/vivekmprac/Maven-Tomcat-Sonar-Nexus.git'
 }
 
 stage('Build')
 {
 sh "${mavenHome}/bin/mvn clean package"
 }
 
  
  stage('ExecuteSonarQubeReport')
  {
  sh "${mavenHome}/bin/mvn sonar:sonar"
  }
 
 stage('UploadArtifactintoNexus')
   {
   sh "${mavenHome}/bin/mvn deploy"
   }
  /* 
   stage('DeployAppIntoTomcatServer')
   {
   sshagent(['1eeb7027-7188-43de-9e65-25569f5190da']) 
   {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.197.144:/opt/apache-tomcat-9.0.37/webapps/"   
   }
   }
   */
    stage('SendEmailNotification')
   {
   emailext body: '''Build is over..

   Regards,
   Mithun Technologies,
   9980923226.''', subject: 'Build is over', to: 'vivekmahendra30@gmail.com'
   }
   
}
 
