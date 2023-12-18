pipeline {
	agent any
	tools{
		maven 'maven3.9'
		
	}
	stages {
		stage('checkoutcode'){
			steps {
				git branch:'main',url: 'https://github.com/Avd-p/java-web-app.git'
				
				

			}
		}
		stage('Build code'){
			steps{
				sh 'mvn clean package'
			}
		}
		stage('Deployment'){
			steps{
				deploy adapters:[tomcat9(url:'http://54.224.84.152:8080/',credentialsld:deployer')] , war:'target/*.war'
			}
		}

	}
}
