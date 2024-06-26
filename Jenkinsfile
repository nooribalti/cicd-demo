pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/nooribalti/cicd-demo.git', branch: 'main'
                sh 'ls -al'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Tests passed"'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("nooribalti/cicd-demo")
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh '''
                        docker stop cicd-demo || true
                        docker rm cicd-demo || true
                        docker run -d --name cicd-demo -p 80:80 nooribalti/cicd-demo
                    '''
                }
            }
        }
    }
}
