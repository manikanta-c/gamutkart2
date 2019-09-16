pipeline {
    agent any

//	tools {
//		maven 'maven3.6'
//	}

//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "mani123" scp /home/mani/.jenkins/workspace/gamutkart2/target/gamutkart.war mani@172.17.0.3:/home/mani/Downloads/apache-tomcat-8.5.38/webapps'
				sh 'sshpass -p "mani123" ssh mani@172.17.0.3 "JAVA_HOME=/home/mani/Downloads/jdk1.8.0_151" "/home/mani/Downloads/apache-tomcat-8.5.38/bin/startup.sh"'
	    	}
		}
    }
}
