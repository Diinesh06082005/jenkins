pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading Code'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flaskapp .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop flask-container || true
                docker rm flask-container || true

                docker run -d \
                --name flask-container \
                -p 5000:5000 \
                flaskapp
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful'
        }

        failure {
            echo 'Deployment Failed'
        }
    }
}