pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t sachin-nginx .
                '''
            }
        }

        stage('Deploy Webpage') {
            steps {
                sh '''
                docker rm -f simple-website || true

                docker run -d \
                  --name simple-website \
                  -p 8081:80 \
                  sachin-nginx
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful"
        }
        failure {
            echo "Deployment failed"
        }
    }
}

