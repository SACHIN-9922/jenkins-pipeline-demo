pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Prepare Files') {
            steps {
                sh '''
                rm -rf /tmp/website
                mkdir -p /tmp/website
                cp index.html /tmp/website/
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
                  -v /tmp/website:/usr/share/nginx/html:ro \
                  nginx
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

