pipeline {
    agent any 
    stages {
        stage('checkout') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
	 stage('build') { 
            steps {
	        echo 'Building Package'
                sh 'mvn package' 
            }
          }
          stage("sonar qube scan") {
            steps {
                sh 'sonar:sonar'
              }
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

