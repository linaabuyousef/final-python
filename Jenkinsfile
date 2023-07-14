pipeline {
    agent any

    environment {
        registry = "linaabuyousef/devopsfinal"
        registryCredential = 'dockerHubCredentials' // Replace with your Docker Hub credentials ID
        dockerImage = ''
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/linaabuyousef/final-python.git']]
                ])
            }
        }

        stage('Build Docker image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":1"
                }
            }
        }

        stage('Push Docker image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push('1')
                    }
                }
            }
        }
    }
}
