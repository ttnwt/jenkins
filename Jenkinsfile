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
	        echo 'Building Package'
                sh 'mvn package' 
            }
        }
        

    }
}

