pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-app"
        CONTAINER_NAME = "my-app-container"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh "docker stop $CONTAINER_NAME || true"
                    sh "docker rm $CONTAINER_NAME || true"
                    sh "docker run -d -p 8081:80 --name $CONTAINER_NAME $IMAGE_NAME"
                }
            }
        }

    }

    post {
        success {
            echo 'Build and Deployment Successful 🚀'
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}
