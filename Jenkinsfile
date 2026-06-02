pipeline {
    agent {
        kubernetes {
            yamlFile 'agent.yaml'
        }
    }

    environment {
        IMAGE_NAME = 'apedreros24/tarea-final'
        IMAGE_TAG = 'arlette-pedreros'
        APP_VERSION = '3.0.0'
        NAMESPACE = 'ns-arlette-pedreros'
        DEPLOYMENT = 'app-arlette-pedreros'
    }

    stages {
        stage('install') {
            steps {
                container('node') {
                    sh '''
                        npm install -g pnpm
                        pnpm install
                    '''
                }
            }
        }

        stage('test') {
            steps {
                container('node') {
                    sh '''
                        pnpm test
                    '''
                }
            }
        }

        stage('build') {
            steps {
                container('docker') {
                    sh '''
                        docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                    '''
                }
            }
        }

        stage('push') {
            steps {
                container('docker') {
                    withCredentials([usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )]) {
                        sh '''
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                            docker push ${IMAGE_NAME}:${IMAGE_TAG}
                        '''
                    }
                }
            }
        }

        stage('deploy') {
            steps {
                container('kubectl') {
                    sh '''
                        kubectl apply -f entrega.yaml
                        kubectl rollout status deployment/${DEPLOYMENT} -n ${NAMESPACE}
                    '''
                }
            }
        }
    }
}
