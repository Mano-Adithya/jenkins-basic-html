pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh "java --varsion"
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

