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
                sh 'mvn package' 
            }
        }
        

    }
}

