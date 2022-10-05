pipeline {
    agent any 
    stages {
        stage('checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
        stage('SonarQube analysis') {
    withSonarQubeEnv(credentialsId: '72d92ffbb85231c9dab6d68055e11b305c0ba56a', installationName: 'sonarqube') { // You can override the credential to be used
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    }
  }
	stage("Quality gate") {
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
