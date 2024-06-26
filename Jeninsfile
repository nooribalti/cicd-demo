pipeline {
    agent {
        docker { image 'node:14' }
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/nooribalti/cicd-demo.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                // Add your test commands here
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
                sh 'echo "Deploying to production"'
                docker stop my-app || true
                docker rm my-app || true
                docker run -d --name my-app -p 3000:3000 your-username/your-repo:latest            }
        }
    }
}
