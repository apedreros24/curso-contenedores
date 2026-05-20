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
        stage('Debug Docker') {
            steps {
                sh '''
                    echo "=== Volumenes Docker activos ==="
                    docker volume ls

                    echo "=== Inspeccion del contenedor Jenkins ==="
                    docker inspect $(hostname) | grep -A 20 "Mounts"
                '''
            }
        }
        stage('CI - Instalacion de dependencias') {
            steps {
                sh '''
                    docker run --rm \
                    --volumes-from $(hostname) \
                    -w $WORKSPACE \
                    ghcr.io/pnpm/pnpm:latest \
                    sh -c "pwd && ls -la && pnpm install"
                '''
            }
        }
    }
}