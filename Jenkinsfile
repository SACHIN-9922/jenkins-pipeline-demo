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
                echo "Stopping any container using port 8081"
                docker ps -q --filter "publish=8081" | xargs -r docker rm -f

                echo "Starting new container"
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

