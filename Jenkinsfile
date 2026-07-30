pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = "github-credentialll"
        DOCKER_IMAGE = "your-dockerhub-username/your-image-name"
        DOCKER_CREDENTIALS = "dockerhub-credential"
    }

    stages {

        stage('Pull Code from GitHub') {
            steps {
                git(
                    url: 'https://github.com/sarakhan481/my-project.git',
                    branch: 'main',
                    credentialsId: "${GITHUB_CREDENTIALS}"
                )
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

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
