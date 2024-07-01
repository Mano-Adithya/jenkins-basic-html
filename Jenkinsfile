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
                    // Configuring AWS CLI using environment variables
                    sh '''
                        aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                        aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                        aws configure set region $AWS_DEFAULT_REGION
                        aws s3 cp index.html s3://s3-jenkins-test
                    '''
                }
            }
        }
    }
}
