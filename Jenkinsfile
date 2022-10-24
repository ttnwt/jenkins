pipeline {
    agent any 
    stages {
        stage('checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
	stage("sonarqube quality scan") {
           steps {
               sh 'mvn sonar:sonar'
            }
        }
	stage("Quality Gate"){

        timeout(time: 10, unit: ‘MINUTES’) {
              def qg= waitForQualityGate()
            if (qg.status!= ‘OK’){
                error “Pipeline aborted due to quality gate failure: ${qg.status}”
            }
        }         
              echo ‘Quality Gate Passed’

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


