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
                    echo "=== Ruta Jenkins ==="
                    echo $WORKSPACE

                    echo "=== Prueba alpine ==="
                    docker run --rm alpine echo "Docker funciona"

                    echo "=== Que ve Docker del volumen ==="
                    docker run --rm -v "$WORKSPACE":/test alpine ls -la /test
                '''
            }
        }
        stage('CI - Instalacion de dependencias') {
            steps {
                sh '''
                    docker run --rm \
                    -v "${WORKSPACE}":/workspace \
                    -w /workspace \
                    ghcr.io/pnpm/pnpm:latest \
                    sh -c "pwd && ls -la && pnpm install"
                '''
            }
        }
    }
}