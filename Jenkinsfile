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
            steps {
                sh 'node --version'
            }
        }

        stage("tercer paso pipeline") {
            steps {
                sh '''
                    echo $DOCKER_HOST
                    docker ps
                '''
            }
        }

    }
}