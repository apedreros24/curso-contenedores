pipeline {
    agent none
    environment{
        IMAGE_NAME = 'curso-contenedores'
        DH_REPO = 'apedreros24/curso-contenedores'
        GH_REPO = 'ghcr.io/apedreros24/curso-contenedores'
    }
    stages{
        stage('CI - de nuestra aplicacion de contenedores'){
            agent{
                docker {
                    image 'node:24-alpine'
                    label 'docker'
                    args '--user root'
                }
            }
            stages{
                stage('CI - Configuracion de pnpm y node'){
                    steps{
                        sh '''
                        npm install -g pnpm
                        pnpm --version
                        '''
                    }
                }
                stage('CI - Instalacion de dependencias'){
                    steps{
                        sh '''
                        pnpm install
                        '''
                    }
                }
                stage('CI - Revision de linter'){
                    steps{
                        sh '''
                        pnpm lint
                        '''
                    }
                }
                stage('CI - Ejecucion de build'){
                    steps{
                        sh '''
                        pnpm build
                        '''
                    }
                }
            }
        }
        stage('CD - Empaquetado y distribucion'){
            agent { label 'docker'}
            steps{
                sh '''
                    docker build -t ${IMAGE_NAME}:latest .
                    docker tag ${IMAGE_NAME}:latest ${DH_REPO}:latest
                    docker tag ${IMAGE_NAME}:latest ${GH_REPO}:latest
                '''
                script{
                    docker.withRegistry('https://index.docker.io/v1/','dh-credencial'){
                        sh 'docker push ${DH_REPO}:latest'
                    }
                    docker.withRegistry('https://ghcr.io','gh-credencial'){
                        sh 'docker push ${GH_REPO}:latest'
                    }
                }
            }
        }
    }
}