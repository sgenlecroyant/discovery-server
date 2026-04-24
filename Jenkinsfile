pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        IMAGE_NAME = "sgenlecroyant/system"
        TAG = "discovery-server-v1"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'pre-develop', url: 'https://github.com/sgenlecroyant/discovery-server.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t $IMAGE_NAME:$TAG .
                """
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(
                        credentialsId: 'docker',
                        usernameVariable: 'USER',
                        passwordVariable: 'PASS'
                )]) {
                    sh """
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE_NAME:$TAG
                    """
                }
            }
        }

    }
}