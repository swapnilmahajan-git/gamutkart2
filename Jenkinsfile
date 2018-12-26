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
			
			script {

		            if (env.ENVIRONMENT='QA'){
					sh 'sshpass -p "gamut" scp target/gamutkart.war gamut@172.17.0.3:/home/gamut/Distros/apache-tomcat-8.5.35/webapps'

					sh 'sshpass -p "gamut" ssh gamut@172.17.0.3 "JAVA_HOME=/home/gamut/Distros/jdk1.8.0_191" "/home/gamut/Distros/apache-tomcat-8.5.35/bin/startup.sh"'
				}
			   else if(env.ENVIRONMENT='SIT'){
					sh 'sshpass -p "gamut" scp target/gamutkart.war gamut@172.17.0.4:/home/gamut/Distros/apache-tomcat-8.5.35/webapps'

					sh 'sshpass -p "gamut" ssh gamut@172.17.0.4 "JAVA_HOME=/home/gamut/Distros/jdk1.8.0_191" "/home/gamut/Distros/apache-tomcat-8.5.35/bin/startup.sh"'
				}
			  }}}
       		
	}

}
