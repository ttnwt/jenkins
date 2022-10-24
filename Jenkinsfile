pipeline {
    agent any 
    stages {
        stage('checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
	//stage("sonarqube quality scan") {
           //steps {
              // sh 'mvn sonar:sonar'
           // }
        //}
	 stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('mysonarqube') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
	stage('Quality gate') { 
            steps {
	        sleep 10
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


