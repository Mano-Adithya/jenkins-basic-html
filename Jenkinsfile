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
                // Perform your build steps here if needed
                sh 'echo "No build steps defined."'
            }
        }

        stage('Deploy Source Artifact') {
            steps {
                echo 'Archiving source code...'
                sh 'zip -r sourceArtif.zip . -x "*" -i "index.html" "README.md" "Jenkinsfile"'
                sh 'aws s3 cp sourceArtif.zip s3://s3-jenkins-test/sourceArtif/sourceArtif.zip'
            }
        }

        stage('Deploy Build Artifact') {
            steps {
                echo 'Deploying build artifact to S3...'
                sh 'zip buildArtif.zip index.html'
                sh 'aws s3 cp buildArtif.zip s3://s3-jenkins-test/buildArtif/buildArtif.zip'
            }
        }
    }
}
