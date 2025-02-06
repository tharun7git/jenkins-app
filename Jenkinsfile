pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/tharun7git/jenkins-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install http-server globally
                    sh 'npm install -g http-server'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Run http-server in the background
                    sh 'nohup http-server ./ -p 8080 > /dev/null 2>&1 &'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
