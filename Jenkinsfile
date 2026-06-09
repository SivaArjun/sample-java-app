pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/SivaArjun/sample-java-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Verify Artifact') {
            steps {
                sh 'ls -ltr target'
            }
        }
    }
}