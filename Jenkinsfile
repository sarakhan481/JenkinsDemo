pipeline {
    agent any

    environment {
        IMAGE_NAME = "sara481khan/jenkinsdemo"
        PATH = "/usr/bin:/usr/local/bin:${env.PATH}"
    }

    stages {

        stage('Pull Code from GitHub') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh '/usr/bin/docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                sh '/usr/bin/docker push $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
