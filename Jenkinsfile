pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIA4MTWLYPXJT6OK3PP')
        AWS_SECRET_ACCESS_KEY = credentials('MbOFwYx9iM80qP/E+Dn3ZO/ZdE3yD+uRJ8BduYs')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh "java --version"
                sh "ls"
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying to S3...'
                script {
                    sh 'echo $AWS_ACCESS_KEY_ID'
                    sh 'echo $AWS_SECRET_ACCESS_KEY'
                    sh 'aws --version'
                    sh "aws s3 cp index.html s3://s3-jenkins-test"
                }
            }
        }
    }
}
