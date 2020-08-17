node {
    def mvnHome = tool name: 'maven3'
    stage('SCM checkout') { // for display purposes
        // Get some code from a GitHub repository
        git credentialsId: 'a4c1e6db-1983-4e35-84e6-2a34930b8bcc', url: 'https://github.com/vivekmprac/Maven-Tomcat-Sonar-Nexus.git'
        // Get the Maven tool.
        // ** NOTE: This 'M3' Maven tool must be configured
        // **       in the global configuration.

    }
    stage('maven Build') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }

       stage('maven sonar') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore sonar:sonar'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore sonar:sonar/)
            }
        }
    }
        stage('nexus deploy') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore deploy'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore deploy/)
            }
        }
    }
            stage('tomcat deploy') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore tomcat7:deploy'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore tomcat7:deploy/)
            }
        }
    }
    stage('SendEmailNotification')
   {
   emailext body: '''Build is over..

   Regards,
   vivek m,
   8197810320.''', subject: 'Build is over', to: 'vivekmahendra30@gmail.com'
   }
}
