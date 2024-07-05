pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    parameters {
        string(name: 'APPLICATION_NAME', defaultValue: 'jen-application', description: 'Name of the CodeDeploy application')
        string(name: 'DEPLOYMENT_GROUP_NAME', defaultValue: 'jen-grp', description: 'Name of the CodeDeploy deployment group')
        string(name: 'S3_BUCKET_NAME', defaultValue: 's3-jenkins-test', description: 'S3 bucket name to store artifacts')
        string(name: 'ARTIFACT_PATH', defaultValue: 'buildArtif/buildArtifact.zip', description: 'Path in S3 bucket to store artifact')
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
                    aws s3 cp buildArtifact.zip s3://${S3_BUCKET_NAME}/${ARTIFACT_PATH}
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
                        --application-name ${APPLICATION_NAME} \
                        --deployment-group-name ${DEPLOYMENT_GROUP_NAME} \
                        --deployment-config-name CodeDeployDefault.OneAtATime \
                        --s3-location bucket=${S3_BUCKET_NAME},key=${ARTIFACT_PATH},bundleType=zip \
                        --region ${AWS_DEFAULT_REGION}
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
            // Add notifications or additional steps here
        }
        failure {
            echo 'Deployment failed.'
            // Add failure handling steps or notifications here
        }
    }
}
