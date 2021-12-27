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

        stage('Build green') {
            steps {
                sh 'echo "Building"'
                sh 'ls -la'
                sh """
                    cd green
                    ls -la
                    docker build -t leoadams/capstone-udacity:${BUILD_NUMBER} .
                """
            }
        }
        stage('Login') {
            steps {
                sh 'echo "Logging"'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Upload image') {
            steps {
                sh 'echo "Uploading"'
                sh 'docker push leoadams/capstone-udacity:${BUILD_NUMBER}'
            }
        }
        stage('Create Infrastructure') {
            // agent {
            //     docker {
            //         image 'amazon/aws-cli'
            //         reuseNode true
            //     }
            // }
            steps {
                sh 'echo "hello aws"'
                sh 'aws --version'
                sh 'echo teste'
                sh 'aws ec2 describe-instances'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}