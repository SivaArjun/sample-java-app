pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                sh '''
                # Clean workspace (optional but recommended)
                rm -rf sample-java-app
                #clone repo using SSH
                git clone git@github.com:SivaArjun/sample-java-app.git

                cd sample-java-app
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                cd sample-java-app 
                mvn clean package
                '''
            }
        }

        stage('Verify Artifact') {
            steps {
                sh '''
                ls -ltr sample-java-app/target
                '''
            }
        }
    }
}