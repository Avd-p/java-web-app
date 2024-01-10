pipeline{
    agent any
    tools{
        maven 'maven3.9'
    }
    stages{
        stage("Checkout Code"){
            steps{
                echo "Code checkout started"
                git branch: 'main', url: 'https://github.com/Avd-p/java-web-app.git'

                echo "Code checkout completed"
            }
        }
        stage("Build Code"){

            steps{
                echo "Code build started"
                sh 'mvn clean package'
                echo "Code build completed"

            }
        }
   stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonar-scanner-meportal'
            }
            steps{
                withSonarQubeEnv('sonar-server-meportal') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }


        
        stage("Deployment"){
            steps{
                deploy adapters: [tomcat9(url: 'http://54.224.84.152:8080/', credentialsId:'deployer')] , war:'target/*.war'
            
            }
        }
    }
}



