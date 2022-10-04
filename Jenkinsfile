pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
	stage('sonar scan') { 
            steps {
                withSonarQubeEnv('SonarQube Scanner') {
                sh 'sonar-scanner'
            }
        }
	stage('Quality Gate') { 
            steps {
                waitForQualityGate abortPipeline: true
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

