pipeline {
    agent any
    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('git checkout') {
            steps {
                sh 'sudo apt update'
                sh 'sudo apt upgrade -y'
                sh 'python3 -v'
            }
        }
        stage('docker version') {
            steps {
                sh 'docker -v'
            }
        }
        stage('install make') {
            steps {
                sh 'sudo apt install make -y'
                sh 'sudo apt install make-guile -y'
            }
        }

        /*
        stage('git checkout') {
            steps {
                git branch: 'master', changelog: false, poll: false, \
                url: 'https://github.com/jaiswaladi246/secretsanta-generator.git'
            }
        }
        stage('compile source code') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('sonarqube analysis') {
            steps {
                sh ''' $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.host.url=http://100.31.95.50:9000 \
                        -Dsonar.login=squ_def98e53a1234fc9b3b2a6ac35ac8d6dcae88fc9 \
                        -Dsonar.projectName=santa \
                        -Dsonar.projectKey=santa \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=.
                '''
            }
        }
        stage('OWASP dependency check') {
            steps {
                dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'ALL' 
                    --prettyPrint''', nvdCredentialsId: 'nvd api key', odcInstallation: 'DP'
        
        dependencyCheckPublisher pattern: 'dependency-check-report.xml'
      }
    }
    stage('build application') {
            steps {
                sh 'mvn clean install -DskipTests=true'
            }
        }
    stage('docker build and push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh 'docker build -t santa .'
                        sh 'docker tag santa miriamoranu/santa'
                        sh 'docker push miriamoranu/santa'
                    }
                }
            }
        }
        stage('trivy scan') {
            steps {
                sh "trivy image miriamoranu/santa"
            }
        }
        stage('docker deploy to container') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh 'docker rm -f santa || true '
                        sh 'docker run -d --name santa -p 8081:8080 miriamoranu/santa'
                    }
                }
            }
        }
        */
    }
}
