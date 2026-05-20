pipeline {
    agent {
        label 'wsl'
    }

    environment {
        DOCKER_HOST = 'unix:///home/apedrero/.docker/desktop/docker.sock'
    }

    stages {
        stage("Primer paso pipeline") {
            steps {
                sh 'echo "saludos desde el terminal"'
            }
        }

        stage("Segundo paso pipeline") {
            agent {
                label 'container'
            }
            steps {
                sh 'node --version'
            }
        }

        stage("Tercer paso pipeline") {
            steps {
                sh '''
                    echo $DOCKER_HOST
                    docker ps
                '''
            }
        }

        stage("Cuarto paso pipeline") {
            agent {
                docker {
                    image 'node:22'
                    label 'wsl'
                    reuseNode true
                }
            }
            steps {
                sh 'node --version'
            }
        }
    }
}