pipeline {
    agent none
    stages {
        stage('CI - de nuestra aplicacion de contenedores') {
            agent {
                docker {
                    image 'node:24-alpine'
                    label 'docker'
                    args '--user root'
                    reuseNode true
                }
            }
            stages {
                stage('CI - Instalacion de dependencias') {
                    steps {
                        sh '''
                            npm install -g pnpm
                            pnpm --version
                            pnpm install
                        '''
                    }
                }
            }
        }
    }
}