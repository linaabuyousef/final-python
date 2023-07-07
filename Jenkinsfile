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
                    sh 'docker run -d --name my-test-container $registry'
                    sh 'sleep 10'
                    sh 'docker logs my-test-container'
                    sh 'docker rm -f my-test-container'
                }
            }
        }
        stage('Push') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        sh 'docker push $registry'
                    }
                }
            }
        }
    }
}
