node{

   def tomcatWeb = '/opt/tomcat/webapps'
   def tomcatBin = '/opt/tomcat/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/lapulga101010/Hellomvn.git'
   }
   stage('Compile'){
      // Get maven home path
      //def mvnHome = tool  name: 'maven-3', type: 'maven'   
      def mvn_version = 'maven-3'
      withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
      sh "mvn clean"
      sh "mvn compile"
      }}
   stage('Test'){
      // Get maven home path
      //def mvnHome =  tool name: 'maven-3', type: 'maven'   
      def mvn_version = 'maven-3'
      withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
      sh "mvn test"
      }
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
     sh "sudo cp ~/.m2/repository/HelloHello.war ${tomcatWeb}/HelloHello.war"
   }
      stage ('Start Tomcat Server') {
         //sleep(time:5,unit:"SECONDS") 
         sh "sudo ${tomcatBin}/startup.sh"
        // sleep(time:100,unit:"SECONDS")
   }
}
