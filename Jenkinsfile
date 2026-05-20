pipeline {
    agent none

    stages{
        stage('CI - de nuestra aplicacion de contenedores'){
            agent{
                docker {
                    image 'node:24'
                }
            }

            stages{
                stage('CI - Instalacion de dependencias'){
                    sh '''
                        pnpm install
                    '''
                }
            }
        }
    }
}