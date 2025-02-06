pipeline {
    agent any

    environment {
        PYTHON_ENV = 'python3'  // Set the Python environment if necessary
        VENV_DIR = 'venv'  // Set the directory for virtual environment
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git repository
                checkout scm
            }
        }

        stage('Set Up Python Environment') {
            steps {
                // Create and activate the virtual environment
                script {
                    sh '''
                        python3 -m venv $VENV_DIR
                        . $VENV_DIR/bin/activate
                    '''
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install required Python dependencies
                script {
                    sh '''
                        . $VENV_DIR/bin/activate
                        pip install --upgrade pip
                        pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run your tests (e.g., using pytest)
                script {
                    sh '''
                        . $VENV_DIR/bin/activate
                        pytest
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (this step depends on your deployment method)
                script {
                    sh '''
                        . $VENV_DIR/bin/activate
                        python deploy.py  // Your deploy script or commands
                    '''
                }
            }
        }
    }

    post {
        always {
            // Clean up actions (e.g., deactivate venv)
            echo 'Cleaning up.'
            sh '''
                . $VENV_DIR/bin/activate || true
                deactivate || true
            '''
        }
    }
}
