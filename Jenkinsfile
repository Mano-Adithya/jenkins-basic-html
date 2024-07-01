pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('')
        AWS_SECRET_ACCESS_KEY = credentials('')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh "java --version"
                sh "ls"
                // No build steps necessary for a simple HTML project
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying to S3...'
                script {
                    sh "aws s3 cp index.html s3://s3-jenkins-test"
                }
            }
        }
    }
}
