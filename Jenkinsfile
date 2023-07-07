pipeline {
    agent any
    environment {
        registry = "linaabuyousef/devopsfinal"
        registryCredential = '0110'
    }
    stages {
       stage('Build') {
            steps {
                bat 'docker build -t %registry% .'
            }
        }
        stage('Test') {
            steps{
                script {
                    bat 'docker run -d --name my-test-container %registry'
                    bat 'sleep 10'
                    bat 'docker logs my-test-container'
                    bat 'docker rm -f my-test-container'
                }
            }
        }
        stage('Push') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        bat 'docker push %registry'
                    }
                }
            }
        }
    }
}
