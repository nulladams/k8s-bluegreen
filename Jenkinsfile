pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Hello') {
            steps {
                sh 'echo "Hello world!"'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Building"'
                sh 'ls -la'
            }
        }
    }
}