pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "your-dockerhub-username/your-image-name"
        DOCKER_CREDENTIALS = "dockerhub-credential"
        GITHUB_CREDENTIALS = "github-credential"
    }

    stages {

        // Stage 1: Pull code from GitHub
        stage('Pull Code from GitHub') {
            steps {
                git(
                    url: 'https://github.com/your-username/your-repository.git',
                    branch: 'main',
                    credentialsId: "${GITHUB_CREDENTIALS}"
                )
            }
        }


        // Stage 2: Build Docker Image
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }


        // Stage 3: Push Image to Docker Hub
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        "${DOCKER_CREDENTIALS}"
                    ) {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
    }
}
