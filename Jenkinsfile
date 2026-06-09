pipeline {
    agent any

    options {
        disableConcurrentBuilds()
        timestamps()
    }

    stages {

        stage('checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Dev') {
            when { branch 'main' }
            steps {
                sh '''
                echo "Deploying to Dev EC2"
                scp target/*.jar ubuntu@<target-65.2.83.230>:/home/ubuntu/app.jar
                ssh ubuntu@<target-65.2.83.230> "pkill -f app.jar || true"
                ssh ubuntu@<target-65.2.83.230> "nohup java -jar /home/ubuntu/app.jar &"
                '''
            }
        }
        stage('Deploy to Staging') {
            when { tag "v*" }
            steps {
                echo "Deploying to Staging"
            }
        }
        stage ('Approval') {
            when { tag "v*"}
            steps {
                input "Approve production deployment"
            }
        }
        stage('Deploy to Production') {
            when { tag "v*" }
            steps {
                echo "Deploying to Production"
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}