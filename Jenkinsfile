pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ibrahimhassan01/nodejs-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'git@github.com:ibrahim-hassan1/nodejs.org.git'
            }
        }


        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image with the build number as tag
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerCredentials') {
                        // Push the image tagged with the build number
                        docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
