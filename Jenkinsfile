node{

   def tomcatWeb = '/opt/apache-tomcat-8.5.54/webapps'
   def tomcatBin = '/opt/apache-tomcat-8.5.54/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/m-k-thakur/jenkinfile.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.sh"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     sh "cp target\JenkinsWar.war \"${tomcatWeb}\JenkinsWar.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
        sh "${tomcatBin}\startup.sh"
         sleep(time:100,unit:"SECONDS")
   }
}
