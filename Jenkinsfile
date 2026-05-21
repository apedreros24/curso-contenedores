pipeline {
    agent {
        label 'docker'
    }
    environment {
        IMAGE_NAME = 'curso-contenedores'
        DH_REPO = 'apedreros24/curso-contenedores'
        GH_REPO = 'ghcr.io/apedreros24/curso-contenedores'
    }
    stages {
        stage('CI - de nuestra aplicacion de contenedores') {
            stages {
                stage('CI - Configuracion de pnpm y node') {
                    steps {
                        sh '''
                            docker run --rm \
                            -v "$WORKSPACE":/workspace \
                            -w /workspace \
                            --user root \
                            node:24-alpine \
                            sh -c "node --version && npm install -g pnpm && pnpm --version"
                        '''
                    }
                }
                stage('CI - Instalacion de dependencias') {
                    steps {
                        sh '''
                            docker run --rm \
                            -v "$WORKSPACE":/workspace \
                            -w /workspace \
                            --user root \
                            node:24-alpine \
                            sh -c "npm install -g pnpm && pnpm install"
                        '''
                    }
                }
                stage('CI - Revision de linter') {
                    steps {
                        sh '''
                            docker run --rm \
                            -v "$WORKSPACE":/workspace \
                            -w /workspace \
                            --user root \
                            node:24-alpine \
                            sh -c "npm install -g pnpm && pnpm lint"
                        '''
                    }
                }
                stage('CI - Ejecucion de build') {
                    steps {
                        sh '''
                            docker run --rm \
                            -v "$WORKSPACE":/workspace \
                            -w /workspace \
                            --user root \
                            node:24-alpine \
                            sh -c "npm install -g pnpm && pnpm build"
                        '''
                    }
                }
            }
        }
        stage('CD - Empaquetado y distribucion') {
            steps {
                sh '''
                    docker build -t ${IMAGE_NAME}:latest .
                    docker tag ${IMAGE_NAME}:latest ${DH_REPO}:latest
                    docker tag ${IMAGE_NAME}:latest ${GH_REPO}:latest
                '''
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dh-credencial') {
                        sh 'docker push ${DH_REPO}:latest'
                    }
                    docker.withRegistry('https://ghcr.io', 'gh-credencial') {
                        sh 'docker push ${GH_REPO}:latest'
                    }
                }
            }
        }
    }
}