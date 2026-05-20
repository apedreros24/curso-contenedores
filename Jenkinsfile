pipeline {
    agent {
        label 'wsl'
    }

    stages {
        stage('CI - Instalacion de dependencias') {
            steps {
                sh '''
                    docker run --rm \
                    -v "$PWD":/app \
                    -w /app \
                    ghcr.io/pnpm/pnpm:latest \
                    sh -c "pnpm runtime set node 24 -g && pnpm --version && pnpm install"
                '''
            }
        }
    }
}