pipeline {
    agent none

    environment {
        DOCKER_HOST = 'unix:///home/apedrero/.docker/desktop/docker.sock'
    }

    stages {
        stage('CI - de nuestra aplicacion de contenedores') {
            agent {
                docker {
                    image 'ghcr.io/pnpm/pnpm:latest'
                    label 'wsl'
                }
            }

            stages {
                stage('CI - Instalacion de dependencias') {
                    steps {
                        sh '''
                            pnpm runtime set node 24 -g
                            pnpm --version
                            pnpm install
                        '''
                    }
                }

                stage('CI - Verificacion') {
                    steps {
                        sh '''
                            node --version
                            pnpm --version
                        '''
                    }
                }
            }
        }
    }
}