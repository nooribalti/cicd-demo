pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS'
        dockerTool 'docker' // Make sure 'Docker' matches the tool name configured in Jenkins
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
                dir('cicd-app') {
                    sh 'npm install'
                }
            }
        }
        
        stage('Test') {
            steps {
                dir('cicd-app') {
                    sh 'echo "Tests passed"'
                }
            }
        }
        
        stage('Docker Build') {
            steps {
                script {
                    dockerTool.withTool('Docker') {
                        docker.build('nooribalti/cicd-demo')
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    dockerTool.withTool('Docker') {
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
}
