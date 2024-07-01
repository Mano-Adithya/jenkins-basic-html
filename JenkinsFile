pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Since this is a simple HTML project, no build steps are necessary
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Here you could add steps to test your HTML files, such as running HTML validation tools
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Here you would add steps to deploy your HTML files
                // For example, copying files to a web server or an S3 bucket
            }
        }
    }
}
