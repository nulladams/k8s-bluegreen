pipeline {
    agent any
    environment {
        CI = 'true'
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
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
                sh """
                    cd blue
                    ls -la
                    docker build -t leoadams/blue:latest .
                """
            }
        }
        stage('Login') {
            steps {
                sh 'echo "Logging"'
                sh 'echo $DOCKERHUB_CREDENTIALS_PWD | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Upload image') {
            steps {
                sh 'echo "Uploading"'
                sh 'docker push leoadams/blue:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}