pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        IMAGE_NAME = "sgenlecroyant/discovery-server"
        TAG = "0.0.1"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'pre-develop', url: 'https://github.com/sgenlecroyant/discovery-server.git'
            }
        }

    }
}