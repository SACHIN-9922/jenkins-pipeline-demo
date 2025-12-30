pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Fetching latest code from GitHub'
                checkout scm
            }
        }

        stage('Deploy Webpage using Docker') {
            steps {
                sh '''
                echo "Stopping old container (if any)"
                docker rm -f simple-website || true

                echo "Starting new container"
                docker run -d \
                  --name simple-website \
                  -p 8081:80 \
                  -v $(pwd):/usr/share/nginx/html \
                  nginx
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful 🚀'
        }
        failure {
            echo 'Deployment failed ❌'
        }
    }
}

