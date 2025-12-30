pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Code fetched from GitHub'
            }
        }

        stage('Deploy Webpage') {
            steps {
                sh '''
                docker rm -f simple-website || true
                docker run -d \
                  --name simple-website \
                  -p 8081:80 \
                  -v $(pwd):/usr/share/nginx/html \
                  nginx
                '''
            }
        }
    }
}

