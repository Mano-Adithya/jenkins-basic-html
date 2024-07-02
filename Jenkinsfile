pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh 'echo "No build steps defined."'
            }
        }

        stage('Package and Upload to S3') {
            steps {
                echo 'Packaging and uploading artifacts to S3...'
                script {
                    sh '''
                    zip -r buildArtifact.zip . -x "*.git*"
                    aws s3 cp buildArtifact.zip s3://s3-jenkins-test/buildArtif/buildArtifact.zip
                    '''
                }
            }
        }

        stage('Deploy with CodeDeploy') {
            steps {
                echo 'Deploying with CodeDeploy...'
                script {
                    sh '''
                    aws deploy create-deployment \
                        --application-name jen-application \
                        --deployment-group-name jen-grp \
                        --deployment-config-name CodeDeployDefault.OneAtATime \
                        --s3-location bucket=s3-jenkins-test,key=buildArtif/buildArtifact.zip,bundleType=zip \
                        --region ap-south-1
                    '''
                }
            }
        }
    }
}
