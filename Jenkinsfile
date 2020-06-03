pipeline {
	agent any

	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			   sh '/home/swapnil/Documents/jenkins-server/apache-maven-3.6.0/bin/mvn install'
	                 }}
		 stage('SonarQube analysis') {
		    steps {
    			withSonarQubeEnv('sonar-6') {
      				sh 'mvn clean package sonar:sonar'
			}} // submitted SonarQube taskId is automatically attached to the pipeline context
  			}
		stage("Quality Gate Status Check"){
		    steps {
         	 	timeout(time: 1, unit: 'HOURS') {
              		def qg = waitForQualityGate()
              		if (qg.status != 'OK') {
                  		error "Pipeline aborted due to quality gate failure: ${qg.status}"
             		 }
         	      }
		    } }   
		stage('Deployment'){
		    steps {
			  sh 'cp target/gamutkart.war /home/swapnil/Documents/jenkins-server/apache-tomcat-8.5.35/webapps'
			}}	
}
}
