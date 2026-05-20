pipeline {
    agent {
        label 'wsl'
    }

    stages {
        stage('CI - Instalacion de dependencias') {
            steps {
                sh '''
                    docker run --rm \
                    -v "$PWD":/workspace/curso-contenedores \
                    -w /workspace/curso-contenedores \
                    ghcr.io/pnpm/pnpm:latest \
                    sh -c "pwd && ls -la && pnpm runtime set node 24 -g && pnpm --version && pnpm install"
                '''
            }
        }
    }
}