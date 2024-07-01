pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
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
