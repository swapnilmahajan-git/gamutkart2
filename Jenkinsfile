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
		stage('Deployment'){
		    steps {
		            sh 'sshpass -p "gamut" scp /home/swapnil/.jenkins/workspace/gamutkart/target/gamutkart.war gamut@172.17.0.3:/home/gamut/Distros/apache-tomcat-8.5.35/webapps'
			  }}
	}
}
