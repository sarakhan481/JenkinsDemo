pipeline {
    agent any

    environment {
        GITHUB_CREDENTIALS = "github-credentialll"
        DOCKER_IMAGE = "sara481khan/jenkinsdemo"
        DOCKER_CREDENTIALS = "dockerhub-creds"
    }

    stages {

        stage('Pull Code from GitHub') {
            steps {
                git(
                    url: 'https://github.com/sarakhan481/jenkinsDemo.git',
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
                        docker.image("${DOCKER_IMAGE}").push("latest")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}
