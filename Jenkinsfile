pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    tools {
        // Define Maven installation configured in Jenkins
        maven 'Maven'
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
                // Run Maven build using configured installation
                sh "mvn clean package"
                // Archive build artifact
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
        
        stage('Deploy Source Artifact') {
            steps {
                echo 'Archiving source code...'
                archiveArtifacts artifacts: '**', allowEmptyArchive: true
                // Optionally, you can also upload source artifacts to S3 or another storage
                // Example: Upload source to S3
                script {
                    sh "aws s3 cp . s3://s3-jenkins-test/source --recursive"
                }
            }
        }

        stage('Deploy Build Artifact') {
            steps {
                echo 'Deploying build artifact to S3...'
                // Example: Deploying a Maven build artifact (JAR file) to S3
                script {
                    sh "aws s3 cp **/target/*.jar s3://s3-jenkins-test/build/"
                }
            }
        }
    }
}
