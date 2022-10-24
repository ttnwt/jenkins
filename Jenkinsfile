pipeline {
    agent any 
    stages {
        stage('checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
	//stage("sonarqube quality scan") {
          //  steps {
            //    sh 'mvn sonar:sonar'
	 stage ("SonarQube analysis") {  
        options {
            timeout(time: 5, unit: 'MINUTES')
            retry(2)
        }
    
        when {
          allOf {
            changeRequest()
          }
        }
      
        steps {
          script {
            STAGE_NAME = "SonarQube analysis"
      
            withSonarQubeEnv('****') {
              sh "../../../sonar-scanner/bin/sonar-scanner"
            }
      
            qualitygate = waitForQualityGate()
            if (qualitygate.status != "OK") {
              currentBuild.result = "FAILURE"
            }
        }
        stage('build') { 
            steps {
	        echo 'packaging'
                sh 'mvn package' 
            }
        }
        stage('Deploy') { 
            steps {
                sh 'scp  /home/ubuntu/.jenkins/workspace/school2022/target/webappbatch2.war   ubuntu@172.31.17.230:/var/lib/tomcat8/webapps/qaenv.war'
            }
        }
    }
}

