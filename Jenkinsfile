node {
   echo 'Hello World**'
   def mvnHome
   def var
   git url: 'https://github.com/Shalini1989/SpringMvcSecurity1.git'
   mvnHome =  tool 'M3'
   stage('checkout/preparation')
   {  
       sh "rm -rf $WORKSPACE/*"	   
       checkout scm
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
    stage('uploadtoRepo'){
       sh '''
	    aws s3 cp /var/lib/jenkins/jobs/CI_Implementation/workspace/target s3://outputs3jenkins/target --recursive
       '''
    }
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
      //  app = docker.build("myimage")
      sh "docker build -t myrepo --rm=true ."
    }
    stage ('Docker push') {
       sh '''
         var=`aws ecr get-login --no-include-email --region us-east-2`
         eval $var
         docker tag myrepo:latest 085396960228.dkr.ecr.us-east-2.amazonaws.com/myrepo:latest
         docker push 085396960228.dkr.ecr.us-east-2.amazonaws.com/myrepo:latest
       '''
    //   docker.withRegistry('https://085396960228.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:demo-ecr-credential')
    //   docker.image('myrepo').push('latest')
  }
    
}
