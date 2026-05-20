pipeline {
    agent {
        label 'container'
    }
    stages{
        stage("Primer paso pipeline") {
            steps{
                sh 'echo "saludos desde el terminal"'
            }
        } 
        stage("Segundo paso pipeline") {
            steps{
                sh 'node --version'
            }
        } 
         stage("tercer paso pipeline") {
            steps{
                sh 'docker ps'
            }
        } 
    }
}