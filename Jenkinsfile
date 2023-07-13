pipeline {
    agent {
        label any
    }
    environment {
        registry = "linaabuyousef/devopsfinal"
        registryCredential = '0110'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/linaabuyousef/final-python.git'
            }
        }
        stage('Build') {
            steps{
                sh "docker build -t ${registry}:${env.BUILD_NUMBER} ."
            }
        }
        stage('Test the Container') {
            steps{
                sh "docker run -itd --name devopsfinal -p 5000:5000 ${registry}:${env.BUILD_NUMBER}"
                sleep 10
                sh 'curl localhost:5000/api/doc'
                sh "docker stop devopsfinal"
                sh "docker rm devopsfinal"
            }
        }
        stage('Push to Docker Hub') {
            steps{
                withCredentials([usernamePassword(credentialsId: registryCredential, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "docker login -u $DOCKER_USER -p $DOCKER_PASS"
                    sh "docker push ${registry}:${env.BUILD_NUMBER}"
                }
            }
        }
    }
}
