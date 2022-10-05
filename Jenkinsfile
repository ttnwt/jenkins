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
                sh 'mvn sonar:sonar'
		echo 'scanning successful'
             }
         }
	 stage('Sonarqube Analysis') {
            environment {
                scannerHome = tool 'Sonar scanner'
            }
            steps {
                withSonarQubeEnv('Sonarserver') {
                    sh "${scannerHome}/bin/sonar-scanner"
                  }
                if ("${json.projectStatus.status}" == "ERROR") {
                            currentBuild.result = 'FAILURE'
                            error('Pipeline aborted due to quality gate failure.')
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
}


