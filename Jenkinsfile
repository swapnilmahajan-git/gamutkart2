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

		stage('Deployment'){
		    steps {
			  sh 'sshpass -p "dev" scp target/gamutkart.war swapnil@172.19.0.1:/home/swapnil/Documents/jenkins-server/apache-tomcat-8.5.35/webapps'
			}}	
}
}
