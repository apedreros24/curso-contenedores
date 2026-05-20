pipeline {
    agent {
        label 'wsl'
    }
    stages {
        stage('Debug workspace') {
            steps {
                sh '''
                    pwd
                    ls -la
                    find . -maxdepth 3 -name package.json
                '''
            }
        }
        stage('CI - Instalacion de dependencias') {
            steps {
                sh '''
                    docker run --rm \
                    -v "$PWD":/app \
                    -w /app \
                    ghcr.io/pnpm/pnpm:latest \
                    sh -c "pwd && ls -la && pnpm install"
                '''
            }
        }
    }
}