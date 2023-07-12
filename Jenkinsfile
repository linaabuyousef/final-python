pipeline {
    agent any
    environment {
        registry = "linaabuyousef/devopsfinal"
        registryCredential = '0110'
    }
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/linaabuyousef/final-python.git' 
            }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Testing image') {
            steps{
                script {
                    def app = docker.run("-p 5000:5000 ${registry}:${BUILD_NUMBER}")
                    sh 'sleep 10' 
                    sh 'curl localhost:5000/api/doc'
                    app.stop() 
                }
            }
        }
        stage('Pushing image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
