pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                git branch: 'main', url: 'https://github.com/ttnwt/jenkins.git'
            }
        }
        stage('build') { 
            steps {
	        input 'Waiting for you to authorize'
                sh 'mvn package' 
            }
        }
        

    }
}

