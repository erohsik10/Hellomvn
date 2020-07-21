node{

   def tomcatWeb = '/opt/tomcat/webapps'
   def tomcatBin = '/opt/tomcat/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/lapulga101010/Hellomvn.git'
   }
   stage('Compile'){
      // Get maven home path
      def mvnHome = '/opt/apache-maven-3.6.3'  name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean"
      sh "${mvnHome}/bin/mvn compile"
      }
   stage('Test'){
      // Get maven home path
      def mvnHome =  tool name: 'maven-3', type: 'maven'   
      sh "${mvnHome}/bin/mvn test"
      
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     sh "cp target\\HelloHello.war ${tomcatWeb}/HelloHello.war"
   }
      stage ('Start Tomcat Server') {
         //sleep(time:5,unit:"SECONDS") 
         sh "${tomcatBin}/startup.sh"
        // sleep(time:100,unit:"SECONDS")
   }
}
