node {
   echo 'Hello World'
   def mvnHome
   def var
   git url: 'https://github.com/debgmail/SpringMvcSecurity.git'
   mvnHome =  tool 'M3'
   stage('checkout/preparation')
   {  
       checkout scm
   }
   stage('end preparation'){
       sh "echo '-------preparation end--------------------------'"
   }
   stage('build') {
      // some block
	  // Run the maven build
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean install"
    }
    stage('Result') {
       archive 'target/*.war'
       junit '**/target/surefire-reports/TEST-*.xml'
    }
    
}