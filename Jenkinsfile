pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/tharun7git/jenkins-app.git'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Start a simple HTTP server to serve the HTML app
                    sh '''
                    # Install http-server if not already installed
                    npm install -g http-server
                    
                    # Serve the HTML app on port 8080
                    http-server ./ -p 8080
                    '''
                }
            }
        }
    }
}
