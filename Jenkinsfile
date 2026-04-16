pipeline {
    agent any

    environment {
    PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin"
    IMAGE_NAME = "sanskriti-app"
    CONTAINER_NAME = "sanskriti-container"

    }

    stages {

        stage('Checkout Code') 
            steps {
                git url: 'https://github.com/sansgupta3010/Sanskriti-Gupta.git', branch: 'main'
            }
        }

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
