pipeline {
    agent any
    
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, \
                url: 'https://github.com/ucheor/python-demo-test.git'
            }
        }
        stage('docker build') {
            steps {
                sh "make image"
            }
        }
        stage('docker push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh 'make push'
                    }
                }
            }
        }
        stage('docker deploy') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh 'docker rm -f python-demo-test-app || true'
                        sh 'docker run -d --name python-demo-test-app -p 8002:5000 miriamoranu/python-demoapp:latest'
                        
                    }
                }
            }
        }
    }
} 