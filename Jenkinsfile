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

        stage('Deploy Source Artifact') {
            steps {
                echo 'Archiving source code...'
                archiveArtifacts artifacts: '**', allowEmptyArchive: true
                script {
                    sh 'aws s3 cp . s3://s3-jenkins-test/sourceArtif --recursive --exclude "*" --include "index.html" --include "README.md" --include "Jenkinsfile"'
                }
            }
        }

        stage('Deploy Build Artifact') {
            steps {
                echo 'Deploying build artifact to S3...'
                script {
                    sh 'aws s3 cp index.html s3://s3-jenkins-test/buildArtif/'
                }
            }
        }
    }
}
