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
                    -v "$WORKSPACE":/workspace \
                    -w /workspace \
                    node:24-alpine \
                    sh -c "npm install -g pnpm && pwd && ls -la && pnpm install"
                '''
            }
        }
    }
}